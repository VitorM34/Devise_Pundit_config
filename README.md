# Devise_Pundit_config
Estarei adicionando um readme explicando como eu fiz a configuracao da gem devise e da gem pundit no ruby. Este documento servirá como guia de estudos e espero estar contribuindo um pouco do meu conhecimento

# Configuração simples do devise dentro de uma aplicação rails
* Para que a gem pundit funcione devemos estar primeiramente com o devise instalado e configurado dentro da nossa aplicação.
* Abaixo irei deixar a configuracao default do devise e também o devise i18n.
* Lembrando que o pundit deve ser instalado e configurado apos a gem devise

#Instalando Devise e o Devise i18n

* passo 1: No terminal rode ```bundle add devise```
* passo 2: rode ```rails generate devise:install```
* passo 3: configurar o action mailer 
  
```ruby
config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
```
* criar um model de user com o comando - ```rails generate devise User```
  - isso cria um  model User (em app/models/user.rb)
  - Logo depois ela cria uma migration no banco
  - Rode rails db:migrate ou se tiver usando docker, docker-compose exec (nome do container) rails db:migrate
*Agora vamos gerar as views do devise com o comando abaixo
```rails generate devise views```
# Rotas e Controllers
* Dentro de routes.rb adicone
  ```ruby
  devise_for :user
  ```
  * agora vamos proteger nosso controller com o comando abaixo:
    
    ```ruby
    class HomeController < ApplicationController
      before_action :authenticate_user!
  
      def index
      # Só acessível se o usuário estiver logado
      end
    end
    ```
* Basicamente nossas views do devise estão configuradas, agora basta usar a estilização de acordo com a sua aplicação rails

# Configurando a Gem I18n para traducoes da nossa aplicacao    

* Passo 1: ```bundle add devise-i18n```
* Passo 2: ```bundle install```
* Pass0 3: Agora abaixo teremos uma configuração simples para traduzir os inputs do devise

* Abra o ```en.yml``` e renomeie para ```pt-BR.yml```
* Agora abaixo irei deixar um arquivo padrão para a configuração da tradução das mensagens do devise, mas lembrando que o mesmo pode ser configurado de acordo com o seu projeto.
  ```yml
  pt-BR:
  activerecord:
    attributes:
      user:
        confirmation_sent_at: Confirmação enviada em
        confirmation_token: Token de confirmação
        confirmed_at: Confirmado em
        created_at: Criado em
        current_password: Senha atual
        current_sign_in_at: Atualmente logado em
        current_sign_in_ip: IP do acesso atual
        email: E-mail
        encrypted_password: Senha criptografada
        failed_attempts: Tentativas sem sucesso
        last_sign_in_at: Último acesso em
        last_sign_in_ip: Último IP de acesso
        locked_at: Bloqueado em
        password: Senha
        password_confirmation: Confirme sua senha
        remember_created_at: Lembrar criado em
        remember_me: Lembre-se de mim
        reset_password_sent_at: Resetar senha enviado em
        reset_password_token: Resetar token de senha
        sign_in_count: Contagem de acessos
        unconfirmed_email: E-mail não confirmado
        unlock_token: Token de desbloqueio
        updated_at: Atualizado em
    models:
      user:
        one: Usuário
        other: Usuários
  devise:
    confirmations:
      confirmed: A sua conta foi confirmada com sucesso.
      new:
        resend_confirmation_instructions: Reenviar instruções de confirmação
      send_instructions: Dentro de minutos, você receberá um email com as instruções de confirmação da sua conta.
      send_paranoid_instructions: Se o seu e-mail existir em nosso banco de dados, você receberá um email com instruções sobre como confirmar sua conta em alguns minutos.
    failure:
      already_authenticated: Você já está autenticado.
      inactive: A sua conta ainda não foi ativada.
      invalid: "%{authentication_keys} ou senha inválidos."
      last_attempt: Você tem mais uma única tentativa antes de sua conta ser bloqueada.
      locked: A sua conta está bloqueada.
      not_found_in_database: "%{authentication_keys} ou senha inválidos."
      timeout: A sua sessão expirou, por favor, faça login novamente para continuar.
      unauthenticated: Para continuar, faça login ou registre-se.
      unconfirmed: Antes de continuar, confirme a sua conta.
    mailer:
      confirmation_instructions:
        action: Confirmar minha conta
        greeting: Bem-vindo %{recipient}!
        instruction: 'Você pode confirmar sua conta através do link abaixo:'
        subject: Instruções de confirmação
      email_changed:
        greeting: Olá %{recipient}!
        message: Estamos entrando em contato para notificá-lo de que seu e-mail está sendo alterado para %{email}.
        message_unconfirmed: Estamos entrando em contato para notificá-lo de que seu e-mail está sendo alterado para %{email}.
        subject: E-mail alterado
      password_change:
        greeting: Olá %{recipient}!
        message: Estamos entrando em contato para notificá-lo de que sua senha foi alterada.
        subject: Senha alterada
      reset_password_instructions:
        action: Redefinir minha senha
        greeting: Olá %{recipient}!
        instruction: Alguém fez o pedido para redefinir sua senha, e você pode fazer isso clicando no link abaixo.
        instruction_2: Se você não fez este pedido, por favor ignore este e-mail.
        instruction_3: Sua senha não será alterada até que você acesse o link acima e crie uma nova.
        subject: Instruções de redefinição de senha
      unlock_instructions:
        action: Desbloquear minha conta
        greeting: Olá %{recipient}!
        instruction: 'Clique no link abaixo para desbloquear sua conta:'
        message: Sua conta foi bloqueada devido ao excessivo número de tentativas acesso inválidas.
        subject: Instruções de desbloqueio
    omniauth_callbacks:
      failure: Não foi possível autorizar de uma conta de %{kind} porque "%{reason}".
      success: Autorizado com sucesso de uma conta de %{kind}.
    passwords:
      edit:
        change_my_password: Alterar minha senha
        change_your_password: Alterar sua senha
        confirm_new_password: Confirme sua nova senha
        new_password: Nova senha
      new:
        forgot_your_password: Esqueceu sua senha?
        send_me_reset_password_instructions: Enviar instruções para redefinição da senha
      no_token: Você não pode acessar esta página sem estar logado. Se você veio de um email de redefinição de senha, por favor certifique-se de ter digitado a URL corretamente.
      send_instructions: Dentro de minutos, você receberá um e-mail com as instruções de redefinição da sua senha.
      send_paranoid_instructions: Se o seu email existir em nosso banco de dados, você receberá um email com um link para recuperação da senha.
      updated: A sua senha foi alterada com sucesso. Você está autenticado.
      updated_not_active: Sua senha foi alterada com sucesso.
    registrations:
      destroyed: Adeus! A sua conta foi cancelada com sucesso. Esperamos vê-lo novamente em breve.
      edit:
        are_you_sure: Você tem certeza?
        cancel_my_account: Cancelar minha conta
        currently_waiting_confirmation_for_email: 'No momento esperando por: %{email}'
        leave_blank_if_you_don_t_want_to_change_it: deixe em branco caso não queira alterá-la
        title: Editar %{resource}
        unhappy: Não está contente?
        update: Atualizar
        we_need_your_current_password_to_confirm_your_changes: precisamos da sua senha atual para confirmar suas mudanças
      new:
        sign_up: Inscrever-se
      signed_up: Bem vindo! Você realizou seu registro com sucesso.
      signed_up_but_inactive: Você se inscreveu com sucesso, porém nós não podemos autenticá-lo porque sua conta ainda não foi ativada.
      signed_up_but_locked: Você se inscreveu com sucesso. Porém nós não podemos autenticá-lo porque sua conta está bloqueada.
      signed_up_but_unconfirmed: Uma mensagem com um link de confirmação foi enviada para o seu e-mail. Por favor, acesse o link para ativar sua conta.
      update_needs_confirmation: Sua conta foi atualizada com sucesso, mas nós precisamos verificar o novo endereço de email. Por favor, verifique seu e-mail e clique no link de confirmação para finalizar confirmando o seu novo e-mail.
      updated: A sua conta foi atualizada com sucesso.
      updated_but_not_signed_in: Sua conta foi atualizada com sucesso, uma vez que sua senha foi alterada será necessário realizar o login novamente.
    sessions:
      already_signed_out: Logout efetuado com sucesso.
      new:
        sign_in: Login
      signed_in: Login efetuado com sucesso.
      signed_out: Logout efetuado com sucesso.
    shared:
      links:
        back: Voltar
        didn_t_receive_confirmation_instructions: Não recebeu instruções de confirmação?
        didn_t_receive_unlock_instructions: Não recebeu instruções de desbloqueio?
        forgot_your_password: Esqueceu sua senha?
        sign_in: Login
        sign_in_with_provider: Entrar com %{provider}
        sign_up: Inscrever-se
      minimum_password_length:
        one: "(Mínimo de %{count} caractere)"
        other: "(Mínimo de %{count} caracteres)"
    unlocks:
      new:
        resend_unlock_instructions: Reenviar instruções de desbloqueio
      send_instructions: Dentro de minutos, você receberá um e-mail com instruções de desbloqueio da sua conta.
      send_paranoid_instructions: Se sua conta existir em nosso banco de dados, você receberá em breve um e-mail com instruções para desbloquear ela.
      unlocked: A sua conta foi desbloqueada com sucesso. Efetue login para continuar.
  errors:
    messages:
      already_confirmed: já foi confirmado
      confirmation_period_expired: É necessário ser confirmado dentro do período %{period}, por favor requisite um novo usuário.
      expired: expirou, por favor solicite uma nova
      not_found: não encontrado
      not_locked: não foi bloqueado
      not_saved:
        one: 'Não foi possível salvar %{resource}: 1 erro'
        other: 'Não foi possível salvar %{resource}: %{count} erros.'
  ```

  # Traduzindo as views

* para traduzir as views pesonalizadas do devise, devemos colocar a seguinte configuração para os campos que são fixos.
* abaixo um exemplo de um label email, onde devemos colocar o t de translate como mostra o nosso exemplo abaixo, para que a gem funcione de maneira correta.
```ruby
<%= f.label :email, t('activerecord.attributes.user.email') %>
<%= f.email_field :email %>
```
* Agora dentro de config/environment/development.rb devemos descomentar a linha ou adionar a seguinte configuração:
  ```ruby
   # Raises error for missing translations.
   config.i18n.raise_on_missing_translations = true
  ```

#Adicionando a gem Pundit 
* Primeiramente devemos rodar o comando dentro do nosso projeto para a adicionar a gem pundit ```bundle add pundit```
* Agora adicionado no Gemfile devemos rodar: ```bundle install```
* Depois disso temos que incluir dentro do nosso controller o Pundit::Authorization como o abaixo:
  ```ruby
  class ApplicationController < ActionController::Base
   include Pundit::Authorization
  end
  ```
* Agora vamos rodar o seguinte comando: ```rails g pundit:install```


