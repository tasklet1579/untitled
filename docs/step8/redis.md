✔️ Redis
```
package nextstep.subway.config;

import ...

@Profile("prod")
@EnableCaching
@Configuration
public class CacheConfig extends CachingConfigurerSupport {
    public static final long DEFAULT_EXPIRE_SECONDS = 60;
    public static final String STATION = "station";
    public static final String LINE = "line";
    public static final String PATH = "path";

    @Autowired
    RedisConnectionFactory connectionFactory;

    @Bean
    public CacheManager redisCacheManager() {
        RedisCacheConfiguration redisCacheConfiguration = RedisCacheConfiguration.defaultCacheConfig()
                                                                                 .serializeKeysWith(RedisSerializationContext.SerializationPair.fromSerializer(new StringRedisSerializer()))
                                                                                 .serializeValuesWith(RedisSerializationContext.SerializationPair.fromSerializer(new GenericJackson2JsonRedisSerializer()));

        Map<String, RedisCacheConfiguration> cacheConfigurations = new HashMap<>();
        cacheConfigurations.put(CacheConfig.STATION, RedisCacheConfiguration.defaultCacheConfig()
                                                                            .entryTtl(Duration.ofHours(CacheConfig.DEFAULT_EXPIRE_SECONDS)));
        cacheConfigurations.put(CacheConfig.LINE, RedisCacheConfiguration.defaultCacheConfig()
                                                                         .entryTtl(Duration.ofHours(CacheConfig.DEFAULT_EXPIRE_SECONDS)));
        cacheConfigurations.put(CacheConfig.PATH, RedisCacheConfiguration.defaultCacheConfig()
                                                                         .entryTtl(Duration.ofHours(CacheConfig.DEFAULT_EXPIRE_SECONDS)));

        RedisCacheManager redisCacheManager = RedisCacheManager.RedisCacheManagerBuilder.fromConnectionFactory(connectionFactory)
                                                                                        .cacheDefaults(redisCacheConfiguration)
                                                                                        .withInitialCacheConfigurations(cacheConfigurations)
                                                                                        .build();
        return redisCacheManager;
    }
}
```
