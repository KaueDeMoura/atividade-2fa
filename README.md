# Cadastro e Verificação de Código com 2FA

Este projeto implementa um sistema de cadastro de usuários com verificação de código de acesso utilizando 2FA (Two-Factor Authentication). O código foi desenvolvido em PHP com integração de banco de dados MySQL e envio de e-mails utilizando a biblioteca PHPMailer.

---

## Funcionalidades

1. **Cadastro de Usuários**: 
   - Os usuários podem se cadastrar fornecendo e-mail e senha.
   - A senha é armazenada como um hash para maior segurança.

2. **Geração de Código de Acesso**:
   - Após o cadastro, um código de acesso é gerado e enviado por e-mail.
   - O código de acesso expira após 10 minutos.

3. **Verificação de Código**:
   - O usuário insere o e-mail e o código recebido para autenticação.
   - O sistema valida o código e verifica se está dentro do prazo de validade.

4. **Banco de Dados**:
   - Armazena usuários com e-mails únicos, senhas, códigos de acesso e timestamps.

---

## Requisitos

- **Servidor**: PHP 7.4 ou superior.
- **Banco de Dados**: MySQL.
- **Composer**: Para gerenciar dependências como o PHPMailer.

---

## Tecnologias Utilizadas

- **PHP**: Lógica do backend.
- **MySQL**: Armazenamento de dados.
- **PHPMailer**: Envio de e-mails via SMTP.
- **HTML/CSS**: Interface simples do usuário.

---

## Configuração

### Banco de Dados
1. Crie o banco de dados e a tabela com o script abaixo:
   ```sql
   CREATE DATABASE IF NOT EXISTS `meu_banco_de_dados`;
   USE `meu_banco_de_dados`;

   CREATE TABLE IF NOT EXISTS `users` (
       `id` INT AUTO_INCREMENT PRIMARY KEY,
       `email` VARCHAR(255) NOT NULL UNIQUE,
       `senha` VARCHAR(255) NOT NULL,
       `codigo_acesso` VARCHAR(255) NOT NULL,
       `codigo_acesso_create_at` TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );
   ```

### Instalar Dependências
1. Certifique-se de que o Composer está instalado.
2. No diretório do projeto, execute:
   ```bash
   composer require phpmailer/phpmailer
   ```

### Configurar PHPMailer
1. No código `register.php`, configure os dados do servidor SMTP:
   ```php
   $mail->Host = 'smtp.gmail.com';
   $mail->SMTPAuth = true;
   $mail->Username = 'seuemail@gmail.com';
   $mail->Password = 'suasenha';
   $mail->SMTPSecure = PHPMailer::ENCRYPTION_STARTTLS;
   $mail->Port = 587;
   ```

---

## Uso

### Cadastro
1. Acesse `register.php` no navegador.
2. Preencha o formulário com e-mail e senha.
3. Um código de acesso será enviado para o e-mail fornecido.

### Verificação
1. Acesse `verify_code.php`.
2. Insira o e-mail e o código de acesso recebido.
3. O sistema verificará o código e fornecerá feedback.

---

## Segurança

- **Hash de Senha**: As senhas são armazenadas usando `password_hash`.
- **Expiração de Código**: O código de acesso expira em 10 minutos.
- **PHPMailer**: Utiliza SMTP seguro com criptografia TLS.
