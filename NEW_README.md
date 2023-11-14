# WebdriverIO Appium Pepino padrão

Projeto Boilerplate para executar testes Appium junto com WebdriverIO e BDD com pepino para:

- Aplicativos nativos iOS/Android
- Aplicativos híbridos iOS/Android

Este projeto foi baseado em [webdriverio/appium-boilerplate](https://github.com/webdriverio/appium-boilerplate/)

> Este modelo usa o aplicativo de demonstração nativo WebdriverIO que, a versão do aplicativo usado neste modelo está na pasta apps, outras versões podem ser encontradas neste link [release](https://github.com/webdriverio/native- aplicativo de demonstração/lançamentos).
> Antes de executar os testes, substitua o aplicativo no diretório `./apps` pelo seu aplicativo.

## Requisitos
- node >= 10.18.x - [como instalar o Node](https://nodejs.org/en/download/)
- yarn >= 1.21.x - [como instalar o Yarn](https://yarnpkg.com/en/docs/install#debian-stable)


## Instalando o Appium em uma máquina local
Consulte [Instalando o Appium em uma máquina local](https://github.com/webdriverio/appium-boilerplate/blob/master/docs/APPIUM.md)

## Configurando Android e iOS em uma máquina local
Para configurar sua máquina local para usar um emulador Android e um simulador iOS, consulte [Configurando Android e iOS em uma máquina local](https://github.com/webdriverio/appium-boilerplate/blob/master/docs/ANDROID_IOS_SETUP.md )

## Começando
Instale as dependências:

```bash
$ instalação de fio
````
Inicie o servidor appium:
```bash
$ aplicativo
```
>O `@wdio/appium-service` está integrado neste modelo para que você não precise iniciar um servidor Appium, o WebdriverIO fará isso para você.

## Configuração
Este padrão usa uma configuração específica para iOS e Android, veja [configs](./config/) e é baseado em `wdio.shared.conf.js`.
Essa configuração compartilhada contém todos os padrões, portanto, as configurações do iOS e do Android só precisam conter os recursos e as etapas necessárias para execução no iOS e/ou Android.

Como não temos o Appium instalado como parte deste pacote, ele foi configurado para usar a instalação global do Appium. Isso está configurado em wdio.shared.conf.js
```
aplicativo: {
     comando: 'appium'
},
```

Neste projeto a aplicação permanece aberta durante a execução de uma suíte e outra, caso seja necessária uma nova sessão ou reinicie a aplicação durante a execução, altere essas configurações no arquivo

```
config.capabilities = [
{
     'appium:noReset': verdadeiro,
     'appium:fullReset': falso,
     'appium:dontStopAppOnReset': verdadeiro,
}
```
Para executar os testes do aplicativo webview você precisa do chromedriver, ele pode ser encontrado [aqui](http://appium.io/docs/en/writing-running-appium/web/chromedriver/), após baixar, edite o arquivo `wdio .android.app.conf.js` e adicione o caminho para a pasta onde está o chromedriver

```
config.capabilities = [
{
     'appium:chromedriverExecutableDir': '<PATH TO CHROME DRIVER>',
}
```
## Línguas faladas
>No diretório `./tets/featuresAndStepsPortuguese/` existem funcionalidades e passos com as palavras-chave em português.

Se quiser usar outro idioma em arquivos de recursos, você pode ver este [doc](https://cucumber.io/docs/gherkin/reference/#spoken-languages) sobre como fazer isso.

## Para executar testes:
```bash
// Para Android
$ fio android.app

//Para iOS
$ fio ios.app
```
## Relatórios
Execute este comando para gerar o relatório allure no diretório `./test-report/allure-report`:

```bash
$ relatório de fio:gerar
```

Você pode executar este comando para iniciar um servidor em sua máquina e abrir o relatório allure no navegador:

```bash
$ relatório de fio:aberto
```
## Eslint e mais bonito
Execute a verificação de lint:

```bash
$ código do fio: verificar
```

Execute o formato lint:

```bash
$ código do fio: formato
```

## Estratégia de localização para aplicativos nativos
A estratégia de localização para este padrão é usar `accessibilityID`'s, consulte também os [documentos do WebdriverIO](http://webdriver.io/guide/usage/selectors.html#Accessibility-ID) ou este boletim informativo no [AppiumPro] (https://appiumpro.com/editions/20).
`accessibilityID`'s facilitam a criação de scripts uma vez e a execução em iOS e Android porque a maioria dos aplicativos já possui alguns `accessibilityID`'s.

Se os `accessibilityID` não puderem ser usados e, por exemplo, apenas o XPATH estiver disponível, então a configuração a seguir poderá ser usada para criar seletores de plataforma cruzada

```js
const SELETORES = {
     WEB_VIEW_SCREEN: navegador.isAndroid
         ? '*//android.webkit.WebView'
         : '*//XCUIElementTypeWebView',
};
```
O mesmo se aplica quando temos o mesmo identificador em ambas as aplicações, mas o comportamento é diferente, para que possamos aplicar funções multiplataforma
```js
     if (driver.isIOS) {
         return expect(cardText).contain(expectedText);
     }
     retornar texto esperado
         .dividir(' ')
         .forEach((palavra) => esperar(cardText).conter(palavra));
     },
```
## Fornecedores de nuvem

### Nuvem de dispositivos reais da Sauce Labs
Este padrão agora também fornece uma configuração para testes com o Real Device Cloud (RDC) da Sauce Labs. Verifique a pasta [SauceLabs](./config/saucelabs) para ver a configuração para iOS e Android.

> Com a versão mais recente do WebdriverIO (`5.4.13` e superior), a configuração do iOS e Android mantém:
> - seleção automática de nuvem RDC dos EUA ou da UE por profissional