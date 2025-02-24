# RFC: Community Care Provider Selection

- Date: 2020-10-01
- Related Issue: https://github.com/department-of-veterans-affairs/va.gov-team/issues/13602
- Associated Problem Statement: https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/products/health-care/appointments/va-online-scheduling/product/product-projects/cc-provider-selection.md

## Background
The VAOS Team would like to provide the ability to automatically find and display eligible community care providers based on proximity 
to a users residential address and to automatically populate input forms with relevant provider address information where required.
This Community Care provider data is currently available from Provider Profile Management System (PPMS) via an integration with VA.gov facilities service. 
The VA.gov Facility Locator tool integrates with PPMS to provide care site information such as address, phone number, and specialties available. 
This integration with PPMS has its limitations and some challenges have been encountered:

1. The data is structured in a way that does not make it easy to query. The first call to PPMS returns a list of care facilities based on proximity using
address or geolocation. A second query is then made for each of the results returned in the first response to fetch phone number, address, and types of 
care available at the facility. This N+1 querying is slow and error prone.

2. There is no mechanism to query by a combination of address and type of care directly via PPMS.

3. There is no way to query by provider name.

## Motivation
We want to have a more performant way of satisfying all three ways that this data might be injested, some supporting use cases specific to Facilities Locator
and others 2 and 3 that might be more specific to VAOS. The VSA Facilities Team, Lighthouse, VAMF, and VAOS have all struggled with some variation of this problem
and there is strong motivation to create a new service that will offer a more performant solution.

## Design

### Infrastrucure Direction

Because this work is likely to be leveraged by teams within VSA, VFS, Lighthouse, VAMF (including the consumers of their APIs) the ideal choice would be to 
address this problem by building a new standalone service outside of the VFS Platform. This would allow each of these platforms to offer their own APIs around 
the service, bring economy of scale in realtime propogation of the new database, more granular metric and performance monitoring for each client utilizing
the new service, with ability to scale horizontally based on utilization of the service independent of VSP as a platform.

VSP Operations has been hard at work building a new container orchestration mechanism that makes it considerably easier to standup:

- a dedicated infrastructure by way of terraform module using ECS/Fargate with RDS and ElasticCache.
- a dedicated CI pipeline using CircleCI configured to a dedicated Github repository.
- metrics and logs fed directly to Datadog and Loki
- errors fed directly to existing VSP Sentry
- dedicated load balanced environments provisioned for dev, staging, and production.

This is a paradigm shift from the monolith philosophy that the VSP Platform has maintained to date. Integrating further things into vets-api that will have to be
be supported and maintained is challenging. It is also taxing on code reviewers that need to prioritize the integrity of platform over individual application
development teams. It is taxing in frequent code reviews. Further, this work encompasses more of a data service with a RESTful API that is likely to be consumed 
in a more application agnostic way than most vets-api application specific APIs. For example, VSA Facilities might utilize certain queries while VAOS might utilize 
certain other queries. Finally, Lighthouse may want to expose this as part of their APIs to consumers outside of the VA or with the VAMF. As such, building as
a standalone service would allow for this service to scale horizontally to meet these demands indepdent of the Platform itself.

### Infrastructure Design

We would leverage the work that VSP Operations has done and standup a docker swarm cluster in AWS Fargate that includes:

- Load Balanced EC2 instance running our Rails or Sinatra application (not yet evaluated, but most likely Rails because we can copy existing code)
- RDS with POSTGIS module available for Geolocation querying
- ElasticCache / Redis for Sidekiq and possibly authentication
- AWS Lambda or Cron for scraping data from PPMS

### Engineering

This should probably live in a separate RFC. But TLDR; We're going to scrape data from PPMS and build our own table optimized in such a way to satisfy the
constraints identified above. We're most likely going to do this with an API only Rails application. Data will be aggregated in one of two ways:

- Initial aggregation of records will be updated in realtime based on client-side requests to the service and populating the database.
- When the database has been primed we can develop more intelligent algorithms for refreshing the local records based on past change history identified.

When we are satisfied with above, we will have a database that updates at least weekly, pulling in updated records sequentially by way of sidekiq worker, cron job,
or AWS Lambda that runs at regular intervals. Details of the engineering work ahead still need to be fleshed out.

## Risks

VSP Operations talent notwithstanding, the work they've done has not been fully vetted by any application teams. They are the subject matter expert there and our
team is not sufficiently staffed to step in and triage should there be an issue. We would essentially be guinea-pigs. That being said, there really isn't anything
particularly new to this model as it's all the same stuff that Vets-API uses and it was recently used in deploying Loki as well.

## Alternatives

We could build this new service as part of vets-api for now and look to make it a stand-alone service in the future. I suspect that this will run into some less
novel challenges in that we're dependent on approval to merge code by VSP since a lot of the work such database migrations, rake tasks, sidekiq workers would
need to be approved.
