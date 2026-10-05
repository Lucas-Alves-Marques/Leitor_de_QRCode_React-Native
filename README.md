# 📱 Leitor de QR Code em React Native

Este projeto foi desenvolvido durante as aulas de Programação Mobile com o objetivo de estudar a construção de um leitor de QR Code em um aplicativo mobile. A aplicação utiliza a câmera do dispositivo para capturar códigos QR e, quando detectado, exibe a informação lida e permite abrir o link caso o conteúdo seja uma URL.

A ideia central do projeto foi praticar o uso de recursos do React Native e da biblioteca Expo Camera para criar uma interface simples, funcional e voltada para leitura de códigos de barra e QR Code em dispositivos móveis.

## 🧠 Objetivo do projeto

O objetivo desta aplicação é:

- estudar o uso de câmera em aplicativos mobile;
- aprender a capturar QR Codes e códigos de barras em tempo real;
- implementar a lógica de digitalização de dados;
- permitir a abertura de links diretamente a partir do conteúdo lido;
- compreender como funciona a interação entre interface, permissão da câmera e processamento dos dados escaneados.

## 📦 Funcionalidades implementadas

### 1. Solicitação de permissão da câmera

Ao iniciar o aplicativo, o código solicita automaticamente permissão para acessar a câmera do dispositivo:

```javascript
const { status } = await Camera.requestCameraPermissionsAsync();
setTemPermissao(status === "granted");
```

Se a permissão for concedida, a câmera é ativada. Caso contrário, a aplicação informa ao usuário que o acesso à câmera não foi permitido.

### 2. Leitura de QR Code e códigos de barras

A aplicação utiliza o componente `CameraView` da biblioteca Expo Camera para a leitura em tempo real:

```javascript
<CameraView
  onBarcodeScanned={digitalizado ? undefined : lidarComCodigoDigitalizado}
  barcodeScannerSettings={{ barcodeTypes: ['qr', 'pdf417'] }}
  style={StyleSheet.absoluteFillObject}
/>
```

Este trecho permite que a aplicação escaneie QR Codes e códigos PDF417. Quando um código é detectado, a função `lidarComCodigoDigitalizado` é acionada.

### 3. Captura do conteúdo digitalizado

Quando o código é lido, o projeto armazena o tipo do código e os dados detectados em estados do React:

```javascript
const [digitalizado, setDigitalizado] = useState(false);
const [dados, setDados] = useState(null);
```

A função responsável pela leitura faz o seguinte:

```javascript
const lidarComCodigoDigitalizado = ({ type, data }) => {
  setDigitalizado(true);
  setDados(data);
  alert(`Codigo de barras do tipo ${type} e dados ${data} foram digitalizados!`);
}
```

Assim, a aplicação registra a informação e exibe um alerta para confirmar a leitura.

### 4. Reescaneamento do código

Depois da leitura, o botão "Toque para digitalizar novamente" aparece para reiniciar o processo de captura:

```javascript
<Button
  color='orange'
  title={"Toque para digitalizar novamente"}
  onPress={() => { setDigitalizado(false) }}
/>
```

Isso permite que o usuário leia outro QR Code sem reiniciar o app.

### 5. Abertura automática de links

Se o conteúdo lido for um endereço de URL, o usuário pode clicar em um botão que abre o link no navegador do dispositivo:

```javascript
const abrirLink = () => {
  Linking.openURL(dados)
}
```

Essa funcionalidade amplia o uso do leitor, tornando possível acessar páginas externas diretamente a partir do QR Code escaneado.

## 🧱 Arquitetura e fluxo da aplicação

A aplicação é simples e funcional, seguindo esse fluxo:

1. solicita acesso à câmera;
2. ativa a leitura em tempo real;
3. detecta o QR Code ou código de barras;
4. armazena os dados lidos;
5. mostra a opção de reescaneamento;
6. possibilita a abertura do link cadastrado no QR Code.

A interface foi criada com componentes básicos do React Native, como `View`, `Text`, `Button` e `StyleSheet`, além do ícone `MaterialCommunityIcons` para representar visualmente o scanner.

## ⚙️ Tecnologias utilizadas

Este projeto utiliza as seguintes tecnologias e bibliotecas:

- React Native: framework para desenvolvimento mobile multiplataforma;
- Expo: ambiente de desenvolvimento e execução para aplicativos React Native;
- Expo Camera: biblioteca utilizada para acessar a câmera do dispositivo e escanear QR Codes;
- JavaScript: linguagem principal do projeto;
- React Hooks: `useState` e `useEffect` para gerenciamento de estado e ciclo de vida;
- Linking: API do React Native para abrir URLs externas;
- Material Community Icons: conjunto de ícones para enriquecer a interface visual.

## 🚀 Como executar o projeto

Para rodar o aplicativo localmente, siga os passos abaixo:

1. Acesse a pasta do projeto:

```bash
cd Leitor_de_QRCode_React-Native
```

2. Instale as dependências:

```bash
npm install
```

3. Inicie o projeto com Expo:

```bash
npx expo start
```

4. Escaneie o QR Code gerado no terminal com o aplicativo Expo Go no celular ou utilize um emulador.

## 🎯 Conclusão

Este projeto foi uma excelente prática para entender a lógica de leitura de QR Code em dispositivos móveis. A aplicação combina câmera, sensores e interação com o usuário para criar uma solução simples e funcional, reforçando conceitos importantes de Programação Mobile e desenvolvimento com React Native.

Além disso, o projeto mostra como é possível transformar um código lido em ação, como abrir um link automaticamente, tornando o uso da tecnologia muito mais intuitivo e aplicável em projetos reais.
