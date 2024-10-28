你可以通过下面的方式定义配置：
```rust
#[derive(Debug, Configurable, Deserialize)]
#[config_prefix = "my-plugin"]
struct Config {
    a: u32,
    b: bool,
}
```

通过[`app.get_config()`](https://docs.rs/spring/latest/spring/app/struct.AppBuilder.html#method.get_config)方法可以读取`toml`中的配置：

```toml
[my-plugin]
a = 10
b = true
```

```rust
struct MyPlugin;

#[async_trait]
impl Plugin for MyPlugin {
    async fn build(&self, app: &mut AppBuilder) {
        // 在自己的插件中加载配置
        let config = app.get_config::<Config>().expect("load config failed");
        //...
    }
}
```

## 在其他插件中使用配置

* [`spring-web`](https://spring-rs.github.io/zh/docs/plugins/spring-web/#du-qu-pei-zhi)
* [`spring-job`](https://spring-rs.github.io/zh/docs/plugins/spring-job/#du-qu-pei-zhi)
* [`spring-stream`](https://spring-rs.github.io/zh/docs/plugins/spring-stream/#du-qu-pei-zhi)