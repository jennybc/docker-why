# docker-why

Quick notes about why an R user would use [Docker](https://www.docker.com), jotted down as I read and thought about responses to [this tweet](https://twitter.com/JennyBryan/status/913785731998289920):

> Has anyone in the #rstats world written really well about the *why* of their use of Docker, as opposed to the *how*?

*This does NOT yet go exhaustively though all the replies, make proper links, etc. Mea culpa.*

Note: I say "Docker" but perhaps I mean ["Linux Containers"](https://en.wikipedia.org/wiki/LXC). I think Docker/DockerHub is to Linux Containers as Git/GitHub is to distributed version control. It's not the only game in town, but it's the most prevalent one today. To push the metaphor even further, [Singularity](http://singularity.lbl.gov) seems to be the [GitLab](https://about.gitlab.com) of Linux Containers.

### Main categories

  * **Educator**: Expert, opinionated R user wants to provide a very specific R environment to other people. Often coupled with using the cloud.
    - Carl B: "I can point them to a URL with RStudio+tidyverse etc ready-to-go on running on an Amazon machine, a XSEDE allocation, or campus cluster". Via DM.
    - Mine and Colin's Duke teaching setup. [Link to PeerJ preprint](https://peerj.com/preprints/3181.pdf).
    - Steph Locke's teaching setup. [blog post](https://itsalocke.com/blog/building-an-r-training-environment/).
  * **Research/Analysis team**: Similar to the Educator approach, a research team wants to share a common environment with the same software (and versions thereof), data sets, etc., and deploy/scale this environment as needed.
     -  Example: Noam's [EHA analysis image](https://github.com/ecohealthalliance/reservoir)
  * **R Package Developer**
    - You have OS A but need to test/debug on OS B (could be a different version of A or an entirely different OS). For certain combinations of A and B, Docker is a way to drop into a running version of B on A. Contrast this with the autopsy reports you get from R CMD check on CRAN, rhub, travis, appveyor. BrodieG example in reply to tweet. [Sean Kross blog post](http://seankross.com/2017/09/17/Enough-Docker-to-be-Dangerous.html). Jim H draft blog post.
      - Note that many of the services mentioned, such as [Travis CI](https://travis-ci.org/) and [R Hub](https://builder.r-hub.io/), are themselves using containers in order to build and test your project on a wide variety of systems.
    - Your normal development setup is A but you need to test/debug with setup B. Actually toggling back and forth is a PITA; it's nicer to use Docker for the setup you use less frequently. Jim H's clang with sanitizers example.
    - You are working in a group of developers, each specialized in some part of a complicated stack necessary to deliver Thing. The different sub-stacks can be containerized to allow everyone to innovate in their domain, to spare everyone from understanding and maintaining everything, and to test Thing when you combine different versions of the sub-components. Rich FitzJohn example via Slack.
     
  * **User of the cloud** Certain things you do require more compute than you have, so you'll pay for compute as needed. Docker is ?the? main way to record/setup the environment you need to be in on this rented "hardware". So you work locally in Docker to interactively develop Thing and then just transfer it to the cloud when it's time to scale up. [Mark Edmondson blog post](http://code.markedmondson.me/rstudio-server-chromebook/)
  * **Nomad**: Your computer(s) is not a physical thing, but rather one or more Docker files. You can instantiate any of your usual computing environments from an internet cafe in the middle of nowhere.
  * **Researcher who values computational reproducibility**: You want to document and share an analysis, with a guarantee that it can be repeated. This is an emerging best practice for scientific publication and some industries, e.g. pharma, may do this to meet regulatory requirements. Therefore, you decide to capture the entire computational environment. Contrast this with the use of packrat or checkpoint to specifically manage the R packages used. This is the use case that has gotten the most attention from a "why?" point of view. Lots of links in the tweet thread.
  * **Other**: wrathematics example of HPC and large scale I/O, tweet.
  
### Connection to other workflows

* Docker with R is currently the [recommended](https://github.com/virtualstaticvoid/heroku-buildpack-r/issues/110) way to deploy R to Heroku, enabling full support for things like Packrat, which the buildpack approach currently does not make possible due to some implementation tricks.

*something about Docker as version control for your computational setup*
  
### Further reading

Lots of excellent resources exist for using Docker. Obviously I feel they cover *how* much better than *why*, hence my question. Good leads for getting started with Docker:

  * PRs for links very welcome here! The tweet thread has many!
