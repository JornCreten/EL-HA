# Enterprise Linux Lab Report

- Student name: Jorn Creten
- Github repo: <https://github.com/HoGentTIN/elnx-2021-ha-JornCreten>


## Requirements

- Enable web page caching

## Test plan

Load tests like always with apache jmeter

## Documentation

First I tried adding the cache through httpd itself, but as it turns out there is not a lot of documentation for this available on the internet and a lot of reported problems with solutions that only half work, or not at all. This pushed me to use varnish as a solution instead of httpd caching. regardless, this is the code that should be added to the httpd cache should you wish to implement it. You will be required to ensure selinux is set up properly to allow httpd to write to the cache.
```
      LoadModule cache_module modules/mod_cache.so
      <IfModule mod_cache.c>
          LoadModule cache_disk_module modules/mod_cache_disk.so
          <IfModule mod_cache_disk.c>
              CacheRoot "c:/cacheroot"
              CacheEnable disk  "/"
              CacheDirLevels 5
              CacheDirLength 3
          </IfModule>

          # When acting as a proxy, don't cache the list of security updates
          CacheDisable "http://security.update.server/update-list/"
      </IfModule>
```

As stated above, I decided to go with varnish. For this I decided to use Jeff Geerling's [varnish role](https://galaxy.ansible.com/geerlingguy/varnish). For the connection between wordpress and varnish a plugin is needed. I decided to go with a plugin that was recommended by wordpress itself, [Proxy cache purge](https://wordpress.org/plugins/varnish-http-purge/). This plugin needs at least php 5.6 so i had to use the remi repository which has access to those versions. This is done in the php role. The plugin itself gets installed through Bert Van Vreckem's [wordpress role](https://galaxy.ansible.com/bertvv/wordpress). It still needs to be activated in the plugins tab of the dashboard after the website is installed.

Varnish routes the "normal" apache served page on port 8080 (moved from port 80 to 8080) through the cache to port 80. The plugin makes it so every time a page is changed it sends a purge request to the cache.


## Test report
Once the plugin is activated, this small menu will appear in the navigation bar. It allows you to clear the cache.
- ![cache](testreports/cacheenabled.png)

To test performance compared to the baseline I re-ran the tests so as to get a good comparison and take as many factors out of the equation.

This is the result of a single webserver with a separate database.
- ![dbtest](testreports/dbtest.png)
- As you can see the results are slightly higher than those recorded in iteration 2. This is why I decided to re-do the tests, as a number of factors could have impacted this.

This is the result of the same webserver with varnish caching enabled. As you can see, the result is massively better than the result without webpage caching and is similar to that of a simple index php page rather than the wordpress application. This is probably because the page is already cached and doesn't need to be processed for every request. The cache will be refreshed every 2 minutes, but this can be changed in the configuration of varnish.
- ![cachetest](testreports/cachedresult.png)



## Resources


- <https://httpd.apache.org/docs/2.4/caching.html>
- <https://www.serverlab.ca/tutorials/linux/web-servers-linux/improve-website-performance-by-enabling-caching-in-apache/>
- <https://www.digitalocean.com/community/tutorials/how-to-configure-apache-content-caching-on-ubuntu-14-04>
- <https://httpd.apache.org/docs/2.4/mod/mod_cache.html#status>
- <https://www.vultr.com/docs/install-varnish-cache-for-apache-on-centos-7>
- <https://www.varnish-software.com/wiki/content/tutorials/wordpress/wp_step_by_step.html#wp-step-by-step> 
- <https://www.elegantthemes.com/blog/wordpress/how-to-use-varnish-with-wordpress>
- <https://www.mercise.ch/installing-php-5-6-on-centos-7-for-wordpress-5-2/>
- <https://galaxy.ansible.com/geerlingguy/varnish>
- <https://wordpress.org/plugins/varnish-http-purge/>