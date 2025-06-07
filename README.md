# -GSI-e-LSI

 Antes de tudo: o que é o DynamoDB?
Imagina um banco de dados super rápido, gerenciado pela AWS, onde você salva documentos em formato de chave e valor, tipo assim:

json
Copiar
Editar
{
  "user_id": "bob",
  "idade": 20,
  "interesses": ["cloud", "rock", "jogos"]
}
Agora, pensa que você quer fazer consultas rápidas, mas sem sempre depender da chave primária. É aí que os danados dos LSI e GSI aparecem. Bora lá! 

LSI – Local Secondary Index
“Eu quero procurar por outros campos, mas SEM mudar minha chave primária!”

O que ele faz?
Ele usa a mesma Partition Key da tabela principal.

Mas deixa você consultar por outros atributos como uma Sort Key alternativa.

Exemplo:
Tabela principal:

Partition Key: user_id

Sort Key: data_criacao

Você cria um LSI pra consultar por idade, mantendo o mesmo user_id como partition key.

LSI = mesmo usuário, jeitos diferentes de organizar a info.

Regras do LSI:
Criado no momento em que a tabela é criada. Não dá pra adicionar depois!

Até 5 LSIs por tabela.

Compartilha o mesmo throughput da tabela principal (ou seja, o mesmo poder de leitura/escrita).

GSI – Global Secondary Index
“Eu quero procurar pelos dados usando uma outra chave completamente diferente.”

O que ele faz?
Permite outra Partition Key + outra Sort Key completamente diferentes da tabela original.

Cria uma cópia customizada dos dados, com a estrutura que você precisa.

Exemplo:
Você quer consultar usuários pela idade em vez do user_id. Cria um GSI com:

Partition Key: idade

Sort Key: nome

Agora você pode fazer buscas por idade de forma rápida!

GSI = liberdade total pra consultar por qualquer campo que quiser.

Regras do GSI:
Pode ser criado a qualquer momento, mesmo depois da tabela existir.

Tem seu próprio throughput separado da tabela principal (paga à parte!).

Máximo de 20 GSIs por tabela (mas raramente você vai querer tantos).

🥷 Resumo Ninja AWS:
Índice	Nome completo	Partition Key	Sort Key	Quando criar?	Compartilha throughput?
LSI	Local Secondary Index	✅ Mesmo da tabela	✅ Diferente	Na criação da tabela	✅ Sim
GSI	Global Secondary Index	❌ Pode ser diferente	✅ Ou não ter	A qualquer momento	❌ Não, é separado

Dica pra lembrar:
🗣LSI = Local = Leva a mesma chave
🗣GSI = Global = Ganha nova chave

