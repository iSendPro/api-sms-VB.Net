# API : Envoi de SMS en Visual Basic .Net
ISendPro Telecom : Envoi de SMS depuis l'API en Visual Basic .Net<br />
https://www.isendpro.com/api-sms/api-envoi-sms-visualbasic-dotnet

## Auteur
ISendPro Telecom<br />
https://www.isendpro.com


## La clé API

L'authentification nécessite une clé API. Cette clé est indispensable car elle vous identifie pour effectuer toutes vos requêtes via notre API SMS.
- Connectez vous à votre compte iSendPro Telecom ici : https://www.isendpro.com/connexion.php
- Cliquez ensuite sur l'onglet "Mon compte" puis sur la sous-rubrique "Mon API"
- Notez votre clé API "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

## Autoriser l'accès

Le contrôle IP permet d'améliorer la sécurité en limitant l'accès à votre clé API. Vous pouvez soit renseigner une liste d'IP autorisées, soit désactiver totalement le contrôle IP.

- Cliquez sur l'onglet "Mon compte" puis sur la sous-rubrique "Mon API"
- Dans la rubrique "Gestion des adresses IP", ajoutez l'adresse IP appelante ou désactivez simplement le contrôle IP.

## Réaliser un premier appel à l'API

- Installer le package isendpro depuis le package Manager Nuget<br />
https://www.nuget.org/packages/iSendProSMS/

    PM> Install-Package iSendProSMS
    

Exemple de script pour l'envoi d'un simple SMS :

    Imports IO.Swagger.Client
    Imports IO.Swagger.Api
    Imports IO.Swagger.Model
    
    Module Module1
    
        Sub Main()
            Dim iapiclient As ApiClient
            Dim keyid As String
            Dim ismsapi As SmsApi
            keyid = "ICI_CLE_API"
            iapiclient = New ApiClient()
            'Envoi de SMS
            ismsapi = New SmsApi(iapiclient)
            Dim susreq = New SmsUniqueRequest()
            susreq.Keyid = keyid
            susreq.Num = "ICI_NUMERO_TELEPHONE"
            susreq.Sms = "Ceci est un test avec un envoi unique !"
            Dim smsreponse As SMSReponse
            smsreponse = New SMSReponse()
            Try
                Console.WriteLine("On oublie" + Chr(10))
                smsreponse = ismsapi.SendSms(susreq)
                Console.WriteLine("json=" + smsreponse.ToJson())
            Catch Exc As Exception
                Console.WriteLine(Exc.ToString())
            End Try
            Console.ReadLine()
    
        End Sub
    
    End Module

Voici le type de réponse attendue aprés l'exécution de ce script :

    {  
       "etat":{  
          "etat":[  
             {  
                "code":0,
                "tel":"06xxxxxxxx",
                "message":"Votre message a bien ete envoye"
             }
          ]
       }
    }

## Les paramètres

Il est possible de spécifier différents paramètres (optionnels) :

- date_envoi :	Date au format YYYY-MM-DD hh:mm. A utiliser uniquement en cas d'envoi différé

- emetteur :	L’émetteur doit être une chaîne alphanumérique comprise entre 4 et 11 caractères. Les caractères acceptés sont les chiffres entre 0 et 9, les lettres entre A et Z et l’espace. Il ne peut pas comporter uniquement des chiffres. Pour la modification de l’émetteur et dans le cadre de campagnes commerciales, les opérateurs imposent contractuellement d’ajouter en fin de message le texte suivant : STOP XXXXX De ce fait, le message envoyé ne pourra excéder une longueur de 149 caractères au lieu des 160 caractères, le « STOP » étant rajouté automatiquement.

- tracker	: Le tracker doit être une chaîne alphanumérique de moins de 50 caractères. Ce tracker sera ensuite renvoyé en paramètre des urls pour les retours des accusés de réception.

- smslong :	Nombre maximum de SMS concaténés que vous autorisez pour l'envoi de ce SMS. Le SMS long permet de dépasser la limite de 160 caractères en envoyant un message constitué de plusieurs SMS. Pour obtenir un calcul dynamique du nombre de SMS alors il faut renseigner smslong = 999

- nostop :	Si le message n’est pas à but commercial, vous pouvez faire une demande pour retirer l'obligation du STOP.

- ucs2 : Il est également possible d'envoyer des SMS en alphabet non latin (russe, chinois, arabe, etc) sur les numéros hors France métropolitaine. Pour ce faire, la requête devrait être encodée au format UTF-8 et contenir l'argument suivant ucs2 = 1 Du fait de contraintes techniques, 1 SMS unique ne pourra pas dépasser 70 caractères (au lieu des 160 usuels) et dans le cas de SMS long, chaque SMS ne pourra dépasser 67 caractères.

## La documentation complète

Ce guide vous a permis d'envoyer votre premier SMS en Visual Basic .Net. Vous pouvez maintenant poursuivre l'intégration de ce service dans votre application. Notre documentation complète vous permettra de découvrir d'autres options pour faciliter l'intégration de services tels que : La consultation du crédit, l'envoi d'un SMS à de multiples destinataires, la qualification d'un numéro (Lookup HLR), téléchargement des récapitulatifs de campagne etc...

Documentation complète : https://www.isendpro.com/api-sms/doc-api-sms-restjson-isendpro.pdf

## Support technique

Si vous avez des questions techniques merci de contacter le support à l’adresse suivante : support@iSendPro.com. Le support technique est joignable tous les jours de la semaine de 9h à 13h et de 14h à 17h.

