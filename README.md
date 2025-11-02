# Bootcamp AWS - Projeto Final CloudFormation

## Descrição
Template final que cria uma instância EC2 Free Tier (t2.micro) com grupo de segurança na região Ohio, configurada com servidor web Apache e página inicial personalizada.

## Status da Pilha
**FinalEC2** - `CREATE_COMPLETE`

## Informações da Pilha
- **Nome da pilha:** FinalEC2  
- **Stack ID:** `arn:aws:cloudformation:us-east-1:661727108851:stack/FinalEC2/168f5360-b833-11f0-815e-0e4560fbb15f`  
- **Região:** Ohio (us-east-1)  
- **Template:** `template-final-ec2.yml`  
- **Tipo de instância:** t2.micro (Free Tier)  
- **Chave SSH:** minha-chave-pessoal  

## Template YAML
```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: Template final - Cria uma instância EC2 Free Tier com grupo de segurança na região Ohio

Resources:
  MeuSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Security group basico para EC2
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: 0.0.0.0/0
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0

  MinhaInstanciaEC2:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: t2.micro
      ImageId: ami-051f8a213df8bc089
      KeyName: minha-chave-pessoal
      SecurityGroups:
        - !Ref MeuSecurityGroup
      UserData:
        Fn::Base64: |
          #!/bin/bash
          sudo yum update -y
          sudo yum install -y httpd
          sudo systemctl start httpd
          sudo systemctl enable httpd
          echo "Servidor Web Ativo! 🚀" > /var/www/html/index.html
```

## Prints da Pilha
### Criada com sucesso
![image](https://github.com/user-attachments/assets/509922b7-0b4c-40fa-9437-48826b6986b1)
![image](https://github.com/user-attachments/assets/b6147b01-0a3c-4871-9e39-ebcd9c46b991)
    

## Observações
- Instância EC2 configurada com Apache.  
- Grupo de segurança liberando portas 22 e 80.  
- Template pronto para deploy em Free Tier AWS.  
