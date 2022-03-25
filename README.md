# Reproduction steps

## Generate csharp-netcore project

Based on the OpenAPI/Swagger petstore example

```sh
openapi-generator generate -i https://raw.githubusercontent.com/swagger-api/swagger-petstore/master/src/main/resources/openapi.yaml -o petstore -g csharp-netcore \
--additional-properties=netCoreProjectFile=true \
--additional-properties=packageName=Petstore \
--additional-properties=targetFramework=net6.0
```

## Add PactNet and replace API test

```sh
cp diff/Petstore.Test.Fix.csproj petstore/src/Petstore.Test/Petstore.Test.csproj
cp diff/PetApiTests.Fix.cs petstore/src/Petstore.Test/Api/PetApiTests.cs
cp diff/XUnitOutput.cs petstore/src/Petstore.Test/Api/XUnitOutput.cs

dotnet build petstore
dotnet test petstore
```