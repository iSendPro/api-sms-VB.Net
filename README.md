# API : Envoi de SMS en Visual Basic .Net
ISendPro Telecom : Envoi de SMS depuis l'API en Visual Basic .Net<br />
https://www.isendpro.com/api-sms/api-envoi-sms-visualbasic-dotnet

## Auteur
ISendPro Telecom<br />
https://www.isendpro.com


## La cl� API

L'authentification n�cessite une cl� API. Cette cl� est indispensable car elle vous identifie pour effectuer toutes vos requ�tes via notre API SMS.
- Connectez vous � votre compte iSendPro Telecom ici : https://www.isendpro.com/connexion.php
- Cliquez ensuite sur l'onglet "Mon compte" puis sur la sous-rubrique "Mon API"
- Notez votre cl� API "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

## Autoriser l'acc�s

Le contr�le IP permet d'am�liorer la s�curit� en limitant l'acc�s � votre cl� API. Vous pouvez soit renseigner une liste d'IP autoris�es, soit d�sactiver totalement le contr�le IP.

- Cliquez sur l'onglet "Mon compte" puis sur la sous-rubrique "Mon API"
- Dans la rubrique "Gestion des adresses IP", ajoutez l'adresse IP appelante ou d�sactivez simplement le contr�le IP.

## R�aliser un premier appel � l'API

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

Voici le type de r�ponse attendue apr�s l'ex�cution de ce script :

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

## Les param�tres

Il est possible de sp�cifier diff�rents param�tres (optionnels) :

- date_envoi :	Date au format YYYY-MM-DD hh:mm. A utiliser uniquement en cas d'envoi diff�r�

- emetteur :	L��metteur doit �tre une cha�ne alphanum�rique comprise entre 4 et 11 caract�res. Les caract�res accept�s sont les chiffres entre 0 et 9, les lettres entre A et Z et l�espace. Il ne peut pas comporter uniquement des chiffres. Pour la modification de l��metteur et dans le cadre de campagnes commerciales, les op�rateurs imposent contractuellement d�ajouter en fin de message le texte suivant : STOP XXXXX De ce fait, le message envoy� ne pourra exc�der une longueur de 149 caract�res au lieu des 160 caract�res, le � STOP � �tant rajout� automatiquement.

- tracker	: Le tracker doit �tre une cha�ne alphanum�rique de moins de 50 caract�res. Ce tracker sera ensuite renvoy� en param�tre des urls pour les retours des accus�s de r�ception.

- smslong :	Nombre maximum de SMS concat�n�s que vous autorisez pour l'envoi de ce SMS. Le SMS long permet de d�passer la limite de 160 caract�res en envoyant un message constitu� de plusieurs SMS. Pour obtenir un calcul dynamique du nombre de SMS alors il faut renseigner smslong = 999

- nostop :	Si le message n�est pas � but commercial, vous pouvez faire une demande pour retirer l'obligation du STOP.

- ucs2 : Il est �galement possible d'envoyer des SMS en alphabet non latin (russe, chinois, arabe, etc) sur les num�ros hors France m�tropolitaine. Pour ce faire, la requ�te devrait �tre encod�e au format UTF-8 et contenir l'argument suivant ucs2 = 1 Du fait de contraintes techniques, 1 SMS unique ne pourra pas d�passer 70 caract�res (au lieu des 160 usuels) et dans le cas de SMS long, chaque SMS ne pourra d�passer 67 caract�res.

## La documentation compl�te

Ce guide vous a permis d'envoyer votre premier SMS en Visual Basic .Net. Vous pouvez maintenant poursuivre l'int�gration de ce service dans votre application. Notre documentation compl�te vous permettra de d�couvrir d'autres options pour faciliter l'int�gration de services tels que : La consultation du cr�dit, l'envoi d'un SMS � de multiples destinataires, la qualification d'un num�ro (Lookup HLR), t�l�chargement des r�capitulatifs de campagne etc...

Documentation compl�te : https://www.isendpro.com/api-sms/doc-api-sms-restjson-isendpro.pdf

## Support technique

Si vous avez des questions techniques merci de contacter le support � l�adresse suivante : support@iSendPro.com. Le support technique est joignable tous les jours de la semaine de 9h � 13h et de 14h � 17h.

