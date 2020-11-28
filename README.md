# nest-microservices-open-api-connector
- A NestJS module for `generator-nest-microservices` yeoman template for connecting your modules to Open API services
### How to use
- install package with `npm i -S nest-microservices-open-api-connector`
- Register the `StorageModule` to your feature modules:
```
@Module({})
export class OpenApiConnectorModule {
  static register(config: ConfigOptions): DynamicModule {
    return {
      module: AppModule,
      imports: [
        OpenApiConnectorModule.register(config.openApiOptions),
        ...
      ],
    };
  }
}
```
- Once `OpenApiConnectorModule` is registered, then you can use `OpenApiService` to upload files to Azure Storage
```
export class ExampleController {
  constructor (private service: OpenApiService) {
    super (service);
  }

  @Get('')
  async getFromExternalService (): Promise<any> {
    return this.service['ExampleApi']['Sample'].findById({ id });
  }
}
```
### Storage options
|Property|Type|Required|Description|
|-|-|-|-|
|hosts|`OpenApiSource[]`|true| Contains { name, url } of the service to connect to
