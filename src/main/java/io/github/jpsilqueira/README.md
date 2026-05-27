Sistema de Checkout e Faturamento Dinâmico (E-Commerce)
Descrição Geral
Este projeto implementa um motor de pagamentos para uma plataforma de e-commerce. A arquitetura garante consistência de dados, evita perda de transações e aplica princípios de programação orientada a objetos para criar um sistema resiliente a falhas.

Como o Sistema Funciona
O sistema opera a partir do arquivo principal, que simula o caixa da loja. O funcionamento segue estas etapas:

Montagem do carrinho: o sistema cria uma lista genérica de pagamentos contendo objetos diferentes, com dados válidos e inválidos.

Processamento contínuo: um laço de repetição percorre a lista. O sistema enxerga apenas a classe pai e aciona o método de processamento genérico.

Resiliência a falhas: blocos de tratamento isolam cada operação. Se um pagamento falhar, o sistema captura a exceção, exibe o erro e prossegue para o próximo cliente sem travar.

Descoberta dinâmica: após aprovar uma transação, o sistema verifica se a classe assina o contrato de emissão de nota. Em caso afirmativo, ele converte o objeto e emite o documento automaticamente.

Explicação do Código
Classe Base e Contratos
FormaPagamento.java: é a base do projeto e não pode ser instanciada diretamente. Ela gerencia os dados fundamentais, como o valor e a situação atual. O construtor impede a criação de pagamentos com valor nulo ou negativo. O método abstrato obriga as classes filhas a definirem suas próprias regras.

EmitenteNotaFiscal.java: define um contrato com um único método de emissão. Serve para indicar quais pagamentos exigem faturamento.

Classes Concretas
PagamentoCartao.java: herda a base e assina o contrato de nota fiscal.

Segurança: os atributos numéricos são finais para garantir imutabilidade.

Processamento: utiliza a estrutura segura do Java para instanciar a conexão com o servidor e rejeita cartões sem limite.

Faturamento: retém os impostos e mascara os números do cartão para exibição.

PagamentoPix.java: herda a base, mas não emite notas.

Segurança: a chave de transferência também é final e imutável.

Processamento: valida se a chave fornecida não está vazia. Caso esteja, interrompe a transação com um erro.

Infraestrutura e Tratamento de Erros
GatewayPagamento.java: simula o servidor da operadora. Implementa a interface de fechamento automático do Java para encerrar a conexão de forma segura ao fim da transação.

SaldoInsuficienteException.java e ChavePixInvalidaException.java: são exceções exclusivas do sistema. Elas diferenciam erros lógicos de negócio de falhas técnicas do computador.

Tecnologias e Conceitos Aplicados
Linguagem: Java.

Imutabilidade: garantia de que dados sensíveis não mudam durante a operação.

Polimorfismo: capacidade de tratar objetos diferentes através de uma origem comum.

Gerenciamento de recursos: uso de blocos nativos para prevenir vazamento de memória.

Como Executar
Agrupe todos os arquivos na mesma pasta ou pacote.

Compile o código-fonte.

Execute a classe principal para visualizar o resultado no terminal.