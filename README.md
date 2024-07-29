## Terraform 101 - AWS

Terraform é uma ferramenta de infraestrutura como código (IaC) que permite definir e provisionar recursos de infraestrutura através de arquivos de configuração. Neste guia, vamos explorar os comandos básicos do Terraform e como utilizá-los para gerenciar recursos na AWS, criando um bucket S3.

### Estrutura de Arquivos

1. **provider.tf**: Define o provedor de nuvem e as configurações associadas.
2. **variables.tf**: Declara as variáveis configuráveis.
3. **terraform.tfvars**: Fornece valores para as variáveis.
4. **resources.tf**: Define os recursos que serão criados.
5. **outputs.tf**: Especifica os outputs após a aplicação do plano.

### Exemplo Prático: Criando um Bucket S3

#### 1. provider.tf

Este arquivo define o provedor AWS e a região.

```hcl
provider "aws" {
  region = "us-west-2"
}
```

#### 2. variables.tf

Declaramos variáveis como o nome do bucket.

```hcl
variable "bucket_name" {
  description = "Nome do bucket S3"
  type        = string
  default     = "my-unique-bucket-name"
}
```

#### 3. terraform.tfvars

Valores específicos para as variáveis.

```hcl
bucket_name = "my-unique-bucket-name"
```

#### 4. resources.tf

Definimos o bucket S3.

```hcl
resource "aws_s3_bucket" "example" {
  bucket = var.bucket_name

  tags = {
    Name = "ExampleBucket"
  }
}
```

#### 5. outputs.tf

Exibe o nome do bucket criado.

```hcl
output "bucket_name" {
  description = "Nome do bucket S3"
  value       = aws_s3_bucket.example.bucket
}
```

### Comandos Básicos do Terraform

1. **`terraform init`**: Inicializa o diretório de trabalho.
2. **`terraform plan`**: Gera um plano de execução.
3. **`terraform apply`**: Aplica o plano, criando recursos.
4. **`terraform validate`**: Valida a configuração.
5. **`terraform destroy`**: Remove os recursos criados.

### HCL (HashiCorp Configuration Language)

HCL, ou HashiCorp Configuration Language, é a linguagem de configuração usada pelo Terraform para definir infraestrutura como código. É uma linguagem declarativa que permite descrever o estado desejado da infraestrutura. Algumas características do HCL incluem:

1. **Legibilidade**: Projetado para ser legível tanto por humanos quanto por máquinas, com uma sintaxe simples e intuitiva.
2. **Blocos e Atributos**: A configuração é organizada em blocos, que podem incluir recursos, variáveis, provedores, etc. Cada bloco contém atributos que definem as propriedades do recurso.
3. **Interpolação**: Permite a utilização de expressões e variáveis para criar configurações dinâmicas.

Exemplo de um bloco de recurso HCL:

```hcl
resource "aws_s3_bucket" "example" {
  bucket = var.bucket_name

  tags = {
    Name = "ExampleBucket"
  }
}
```

### Arquivos Gerados Após `terraform init`

Após a execução do comando `terraform init`, alguns arquivos e diretórios importantes são gerados no diretório de trabalho. Esses arquivos são usados pelo Terraform para gerenciar o estado da infraestrutura e os plugins necessários.

1. **.terraform/**: Um diretório que contém os plugins e módulos necessários para o Terraform se comunicar com os provedores de infraestrutura. Ele também armazena informações sobre o back-end que está sendo usado para gerenciar o estado.

2. **.terraform.lock.hcl**: Um arquivo de bloqueio que garante a consistência dos plugins usados. Ele registra as versões exatas dos plugins que foram instalados, para garantir que as futuras execuções usem as mesmas versões e evitar mudanças inesperadas na infraestrutura.

3. **terraform.tfstate** (e **terraform.tfstate.backup**): Após a execução de `terraform apply`, o Terraform gera um arquivo `terraform.tfstate`, que armazena o estado atual da infraestrutura. Esse arquivo é crucial, pois o Terraform o utiliza para determinar o que precisa ser criado, atualizado ou excluído na próxima execução. O arquivo `.backup` é uma cópia de segurança do estado anterior.

4. **terraform.tfvars.lock.hcl**: Um arquivo opcional que pode ser gerado dependendo da configuração de variáveis e a utilização de módulos. Ele pode conter informações sobre as variáveis e módulos bloqueados para garantir consistência.

### Conclusão

Este exemplo demonstra como usar o Terraform para criar um bucket S3 na AWS, introduzindo a estrutura de arquivos e comandos principais. É um bom ponto de partida para entender como o Terraform funciona e como ele pode ser usado para gerenciar infraestrutura na nuvem.

Esses arquivos e diretórios são essenciais para o funcionamento do Terraform, permitindo o gerenciamento eficiente e seguro da infraestrutura como código. Eles ajudam a garantir que as mudanças sejam previsíveis e consistentes, facilitando a manutenção e a colaboração em projetos de infraestrutura.