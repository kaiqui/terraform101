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

### Conclusão

Este exemplo demonstra como usar o Terraform para criar um bucket S3 na AWS, introduzindo a estrutura de arquivos e comandos principais. É um bom ponto de partida para entender como o Terraform funciona e como ele pode ser usado para gerenciar infraestrutura na nuvem.