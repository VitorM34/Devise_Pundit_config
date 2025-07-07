# Devise_Pundit_config
Estarei adicionando um readme explicando como eu fiz a configuracao da gem devise e da gem pundit no ruby. Este documento servirá como guia de estudos e espero estar contribuindo um pouco do meu conhecimento

#Configuração simples do devise dentro de uma aplicação rails
* Para que a gem pundit funcione devemos estar primeiramente com o devise instalado e configurado dentro da nossa aplicacao.
* Abaixo irei deixar a configuracao default do devise e também o devise i18n.
* Lembrando que o pundit deve ser instalado e configurado apos a gem devise

#Instaland o Devise e Devise i18n

passo 1: No terminal rode bundle add devise 
passo 2: rode rails generate devise:install
passo 3: configurar o action mailer 
///config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }///
