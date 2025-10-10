[CLI Prerequisites](https://github.com/swagger-api/swagger-codegen/blob/master/docs/prerequisites.md)

Install for Linux:
```shell
# Download current stable 3.x.x branch (OpenAPI version 3)
wget https://repo1.maven.org/maven2/io/swagger/codegen/v3/swagger-codegen-cli/3.0.71/swagger-codegen-cli-3.0.71.jar -O swagger-codegen-cli.jar

java -jar swagger-codegen-cli.jar --help

# Create a command from it
mkdir ~/tools
mv swagger-codegen-cli.jar tools

# Inside .zshrc
alias swagger-codegen="java -jar ~/tools/swagger-codegen-cli.jar"

# Restart ZSH
source .zshrc
```

How to use it:
```shell
usage: swagger-codegen [-h] Command ...

named arguments:
  -h, --help             show this help message and exit

commands:
  Command                additional help
    generate             generate
    config-help          config-help
    meta                 meta
    langs                langs
    version              version
```

Command:
```shell
swagger-codegen generate -i src/main/resources/api.yaml -l spring -o ./generated
```