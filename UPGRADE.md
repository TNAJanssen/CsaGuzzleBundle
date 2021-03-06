UPGRADE documentation
=====================

* Upgrade [from 1.0 to 1.1](UPGRADE-1.1.md)
* Upgrade [from 1.1 to 1.2](UPGRADE-1.2.md)
* Upgrade [from 1.2 to 1.3](UPGRADE-1.3.md)

UPGRADE FROM 1.0 to 1.1 [from 1.0 to 1.1]
-----------------------------------------

### Known Backwards-Compatibility Breaks

* If you use the `Csa\Bundle\GuzzleBundle\Factory\Client`, the class was removed as it is no longer needed.

  You should now use the base `GuzzleHttp\Client` class, or your own class, extending Guzzle's class.

* If you registered event subscribers using the compiler pass, you now need to give it an alias.

Before:

```xml
<container>
    <services>
        <service id="acme_demo.subscriber.custom" class="Acme\DemoBundle\Guzzle\Subscriber\CustomSubscriber">
            <tag name="csa_guzzle.subscriber" />
        </service>
    </services>
</container>
```

After:


```xml
<container>
    <services>
        <service id="acme_demo.subscriber.custom" class="Acme\DemoBundle\Guzzle\Subscriber\CustomSubscriber">
            <tag name="csa_guzzle.subscriber" alias="acme_custom" />
        </service>
    </services>
</container>
```

UPGRADE FROM 1.1 to 1.2 [from 1.1 to 1.2]
-----------------------------------------

### Known Backwards-Compatibility Breaks

* None yet

UPGRADE FROM 1.2 to 1.3 [from 1.2 to 1.3]
-----------------------------------------

### Known Backward-Compatibility Breaks

* `ClientFactory` was deprecated in favor of directly tagging Guzzle clients,
  and will be removed in 2.0.

  Before:

  ```xml
  <service
          id="acme.client"
          class="%acme.client.class%"
          factory-service="csa_guzzle.client_factory"
          factory-method="create">
      <!-- An array of configuration values -->
  </service>
  ```

  After:

  ```xml
  <service id="acme.client" class="%acme.client.class%">
      <tag name="csa_guzzle.client" />
  </service>
