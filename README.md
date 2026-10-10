# Calculadora de IMC em Flutter

Aplicação mobile em Flutter para calcular o Índice de Massa Corporal (IMC) a partir do peso e da altura informados pelo usuário.

## Objetivo da aula

Ensinar, de forma prática e didática, os conceitos básicos de:

- criação de interfaces com Flutter
- uso de widgets como `TextField`, `Form`, `RaisedButton` e `Text`
- manipulação de estados com `StatefulWidget`
- validação de formulário
- lógica de cálculo do IMC
- execução e teste da aplicação em emulador ou dispositivo

## Funcionalidades

- entrada de peso em quilogramas
- entrada de altura em centímetros
- validação dos campos
- cálculo do IMC
- classificação do resultado conforme a tabela padrão:
  - Abaixo do peso
  - Peso normal
  - Sobrepeso
  - Obesidade grau 1
  - Obesidade grau 2
- botão para limpar os campos

## Tecnologias utilizadas

- Flutter
- Dart
- Material Design

## Estrutura do projeto

```text
calculadora-imc-flutter/
├── android/
├── ios/
├── lib/
│   └── main.dart
├── test/
├── .gitignore
├── .metadata
├── pubspec.yaml
├── README.md
└── pubspec.lock
```

## Pré-requisitos

Antes de começar a aula, certifique-se de que o ambiente está preparado:

1. Instalar o Flutter SDK
2. Verificar a instalação com:

```bash
flutter doctor
```

3. Ter o Android Studio ou VS Code instalado
4. Configurar um emulador Android ou conectar um dispositivo físico
5. Confirmar que o ambiente está pronto com:

```bash
flutter --version
```

## Como executar o projeto

No terminal, dentro da pasta do projeto, execute:

```bash
flutter pub get
flutter run
```

Se quiser abrir em um emulador específico, primeiro liste os dispositivos disponíveis:

```bash
flutter devices
```

## Procedimento didático para a aula (passo a passo)

### 1. Apresentação do problema

Explique ao aluno que a aplicação será uma calculadora de IMC, uma ferramenta muito utilizada para avaliar a relação entre peso e altura.

Perguntas para instigar a atenção:

- Como uma aplicação pode receber dados do usuário?
- Como transformar esses dados em um cálculo?
- Como exibir o resultado de forma clara?

### 2. Explicação do conceito de IMC

Apresente a fórmula:

```text
IMC = peso / (altura em metros × altura em metros)
```

Exemplo:

- peso: 70 kg
- altura: 1,75 m
- IMC = 70 / (1,75 × 1,75) = 22,86

Comente que o resultado é classificado em faixas, como:

- abaixo de 18,5: abaixo do peso
- 18,5 a 24,9: peso normal
- 25,0 a 29,9: sobrepeso
- 30,0 a 34,9: obesidade grau 1
- acima de 35: obesidade grau 2

### 3. Estrutura da interface

Mostre os principais widgets que serão usados:

- `Scaffold`: estrutura base da tela
- `AppBar`: barra superior
- `TextFormField`: campos de entrada
- `RaisedButton`: botão de calcular
- `Text`: exibição do resultado
- `Icon`: ícone representativo

Explique que a tela terá:

- título da app bar
- campo para peso
- campo para altura
- botão para calcular
- texto com o resultado
- botão de limpar

### 4. Criação do projeto Flutter

Se a aula for iniciada do zero, execute:

```bash
flutter create calculadora_imc
cd calculadora_imc
```

Depois abra a pasta no editor e localize o arquivo:

```text
lib/main.dart
```

### 5. Implementação do widget principal

Crie uma tela com `StatefulWidget`, pois a interface precisa reagir às mudanças dos campos de entrada.

Exemplo de organização:

```dart
class Home extends StatefulWidget {
  @override
  _HomeState createState() => _HomeState();
}
```

Explicação:

- `StatefulWidget` permite atualizar a tela quando o usuário digita ou clica no botão
- o estado guarda os valores e o texto do resultado

### 6. Criação dos controladores de texto

Adicione os campos de entrada:

```dart
TextEditingController weightController = TextEditingController();
TextEditingController heightController = TextEditingController();
```

Explique que esses controladores capturam o que o usuário digita e permitem manipular o valor programaticamente.

### 7. Validação do formulário

Use `Form` e `GlobalKey<FormState>` para validar se os campos não estão vazios.

Exemplo:

```dart
if (value.isEmpty) {
  return "Insira seu peso";
}
```

Ensine os alunos que validação é importante para evitar erros e melhorar a experiência do usuário.

### 8. Lógica do cálculo do IMC

No método de cálculo, faça:

```dart
double weight = double.parse(weightController.text);
double height = double.parse(heightController.text) / 100;
double imc = weight / (height * height);
```

Explique:

- a altura digitada em centímetros é convertida para metros
- o cálculo usa a fórmula do IMC
- o valor é exibido com `toStringAsPrecision(3)` para manter uma leitura mais limpa

### 9. Classificação do resultado

Use condicionais (`if`/`else if`) para definir a classificação:

```dart
if (imc < 18.5) {
  _infoText = "Abaixo do peso";
} else if (imc >= 18.5 && imc <= 24.9) {
  _infoText = "Peso normal";
} else if (imc >= 25.0 && imc <= 29.9) {
  _infoText = "Sobrepeso";
}
```

### 10. Limpeza dos campos

Crie a função `reset` para limpar os valores do formulário:

```dart
void _resetFields() {
  weightController.text = "";
  heightController.text = "";
  setState(() {
    _infoText = "Informe seus dados";
  });
}
```

Explique que esse recurso melhora a usabilidade da aplicação.

### 11. Execução da aplicação

No terminal, rode:

```bash
flutter run
```

Oriente os alunos a:

- abrir o emulador
- testar com valores diferentes
- verificar as mensagens e o comportamento dos campos
- conferir a resposta do cálculo

### 12. Teste prático com dados

Peça para os alunos testarem os valores abaixo:

- peso: 65 kg / altura: 170 cm → IMC ≈ 22,49 → peso normal
- peso: 80 kg / altura: 170 cm → IMC ≈ 27,68 → sobrepeso
- peso: 55 kg / altura: 160 cm → IMC ≈ 21,48 → peso normal
- peso: 90 kg / altura: 165 cm → IMC ≈ 33,06 → obesidade grau 1

### 13. Discussão final

Perguntas para encerramento:

- Qual a diferença entre estado local e estado global?
- Por que usar `Form` em vez de apenas `TextField`?
- Como a validação melhora a aplicação?
- Quais outros projetos podem usar esse mesmo padrão?

## Dicas para a aula

- Utilize exemplos reais do cotidiano para contextualizar o cálculo
- Mostre a lógica em blocos pequenos e vá testando a cada etapa
- Incentive a utilização do emulador para visualização imediata
- Ajuste a interface com cores e ícones para deixar a aula mais visual
- Peça que os alunos modifiquem a mensagem final ou adicionem mais categorias

## Referências

- [Documentação oficial do Flutter](https://flutter.dev/docs)
- [Flutter Codelabs](https://flutter.dev/docs/get-started/codelab)
- [Material Design](https://material.io/design)

## Conclusão

Esta aplicação mostra como construir uma interface simples e funcional em Flutter, integrando entrada de dados, validação, cálculo e apresentação de resultado. É um ótimo projeto para aulas introdutórias de desenvolvimento mobile.

## Autor

Projeto desenvolvido como exemplo didático para aula de Flutter.

## Licença

Este projeto foi criado para fins educacionais.
