---
title: Form
form:
    name: contact-form
    fields:
        - name: name
          label: Nome
          placeholder: 'Digite seu nome'
          autofocus: true
          autocomplete: on
          type: text
          validate:
              required: true

        - name: email
          label: Email
          placeholder: 'Digite seu email'
          type: email
          validate:
              required: true

        - name: message
          label: Mensagem
          placeholder: 'Escreva sua mensagem'
          type: textarea
          validate:
              required: true

    buttons:
        - type: submit
          value: Enviar
        - type: reset
          value: Limpar

    process:
        - save:
            fileprefix: contato-
            dateformat: Ymd-His-u
            extension: txt
            body: "{% include 'forms/data.txt.twig' %}"
        - email:
            from: '{{ form.value.email }}'
            to: 'felipeemonari@gmail.com'
            subject: '[Formulário Grav] Nova mensagem de {{ form.value.name }}'
        - message: 'Obrigado! Sua mensagem foi enviada com sucesso!'
        - display: thank-you
---