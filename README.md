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
