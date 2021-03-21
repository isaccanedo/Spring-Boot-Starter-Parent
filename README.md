# Spring Boot Parent

# 1. Introdução
Neste tutorial, aprenderemos sobre spring-boot-starter-parent e como podemos nos beneficiar disso para melhor gerenciamento de dependências, configurações padrão para plug-ins e construir rapidamente nossos aplicativos Spring Boot.

Também veremos como podemos substituir as versões das dependências e propriedades existentes fornecidas pelo starter-parent.

# 2. Spring Boot Starter Parent
O projeto spring-boot-starter-parent é um projeto inicial especial - que fornece configurações padrão para nosso aplicativo e uma árvore de dependência completa para construir rapidamente nosso projeto Spring Boot.

Ele também fornece configuração padrão para plug-ins Maven, como maven-failafe-plugin, maven-jar-plugin, maven-surefire-plugin, maven-war-plugin.

Além disso, ele também herda o gerenciamento de dependências de spring-boot-dependencies que é o pai do spring-boot-starter-parent.

Podemos começar a usá-lo em nosso projeto adicionando this como um pai no pom.xml do nosso projeto:

```
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.4.0</version>
</parent>
```

Sempre podemos obter a versão mais recente do spring-boot-starter-parent no Maven Central.

# 3. Gerenciando Dependências
Depois de declarar o pai inicial em nosso projeto, podemos extrair qualquer dependência do pai apenas declarando-a em nossa tag de dependências.

Além disso, não precisamos definir as versões das dependências, o Maven baixará os arquivos jar com base na versão definida para o pai inicial na tag pai.

Por exemplo, se estamos construindo um projeto da web, podemos adicionar spring-boot-starter-web diretamente e não precisamos especificar a versão:

```
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

# 4. A Tag de Gerenciamento de Dependências
Para gerenciar uma versão diferente de uma dependência fornecida pelo pai inicial, podemos declarar a dependência e sua versão explicitamente na seção dependencyManagement:

```
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
            <version>2.4.0</version>
        </dependency>
    </dependencies>
</dependencyManagement>
```

# 5. Propriedades
Para alterar o valor de qualquer propriedade definida no pai inicial, podemos declará-lo novamente em nossa seção de propriedades.

O spring-boot-starter-parent por meio de seu pai spring-boot-dependencies usa propriedades para configurar todas as versões de dependências, versão Java e versões de plug-in Maven.

Portanto, é fácil para nós controlar essas configurações, apenas alterando a propriedade correspondente.

Se quisermos alterar a versão de qualquer dependência que desejamos extrair do pai inicial, podemos adicionar a dependência na tag de dependência e configurar diretamente sua propriedade:

```
<properties>
    <junit.version>4.11</junit.version>
</properties>
```

# 6. Outras substituições de propriedade
Também podemos usar propriedades para outras configurações, como gerenciamento de versões de plug-ins ou até mesmo para alguma configuração básica, como gerenciamento da versão Java, codificação de origem.

Só precisamos declarar novamente a propriedade com um novo valor.

Por exemplo, para alterar a versão Java, podemos indicá-la na propriedade java.version:

```
<properties>
    <java.version>1.8</java.version>
</properties>
```

# 7. Projeto Spring Boot sem o pai inicial

Às vezes, temos um pai Maven personalizado. Ou podemos preferir declarar todas as nossas configurações Maven manualmente.

Nesse caso, podemos optar por não usar o projeto spring-boot-starter-parent. Mas, ainda podemos nos beneficiar de sua árvore de dependências adicionando uma dependência spring-boot-dependencies em nosso projeto no escopo de importação.

Vamos explicar isso com um exemplo simples no qual queremos usar outro pai que não seja o pai inicial:

```
<parent>
    <groupId>com.isac</groupId>
    <artifactId>spring-boot-parent</artifactId>
    <version>1.0.0-SNAPSHOT</version>
</parent>
```

Aqui, usamos módulos-pai em um projeto diferente como nossa dependência pai.

Agora, neste caso, ainda podemos obter os mesmos benefícios do gerenciamento de dependência, adicionando-o no escopo de importação e tipo de pom:

```
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-dependencies</artifactId>
            <version>2.2.6.RELEASE</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

Além disso, podemos obter qualquer dependência apenas declarando-a nas dependências, como fizemos em nossos exemplos anteriores. Nenhum número de versão é necessário para essas dependências.

# 8. Resumo
Neste tutorial, demos uma visão geral do spring-boot-starter-parent e o benefício de adicioná-lo como um pai em qualquer projeto filho.

Em seguida, aprendemos como gerenciar dependências. Podemos substituir dependências em dependencyManagement ou por meio de propriedades.

O código-fonte dos trechos usados neste tutorial está disponível aqui https://github.com/isaccanedo/Spring-Boot-Starter-Parent, um usando o pai inicial e o outro um pai personalizado.
