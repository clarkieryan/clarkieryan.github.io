---
title:  "A/B testing with Angular & Optimizely"
date:   2017-02-10 15:04:23
categories: [javascript]
tags: [javascript]
---
A/B Testing a SPA can be quite difficult especially when you are unable to deploy as often as you like. Over at betsson I work with 7 different brands on a single codebase, deploying those configurations can be quite slow and approvals can be a slow process. But with A/B testing we need to be able to constantly test variations to the sites and react to this. 

As part of this multiple brands on a single codebase we currently have quite a sophisticated config file for each brand allowing us to turn on/off features and edit a number of items inside of features such as stylings and content. The vital ones are loaded as part of the index.html - but a lot of these are loaded from an API call. 

So we needed a solution to be able to choose a specific configuration for the user. The best solution for this is to have a md5 hash of a configration injected into our webpage for whatever test we need. 

So we ended up with the following angular service below;

``` javascript
class ConfigurationService {
  /*@ngInject*/
    constructor(
        private configurationServer
        private $window
    ){

  }

    public getCurrentConfiguration(){
        return {...this.defaultConfiguration(), ...this.optimizelyConfiguration()}
    }

    private defaultConfiguration(): Object{
        return this.defaultConfiguration;
    }

    private optimizelyConfiguration(): Object{
        var hash = this.$window.optimizelyConfigurationHash;
        var configuration = this.getCustomConfiguration(hash);

        return configuration;
    }

    private getCustomConfigration(key){
        return this.configurationServer.getConfiguration(key);
    }

}
```

By doing this you can literally inject anything, we even plan on being able to override HTML partials!