# Custom Phishing

- **Server**: AWS EC2:

- Gopish (*:3333*)
- Custom BACK (*:443*):

###### Components

En este punto los componentes escenciales relacionados son:

- *Gopish*: ([Documentation](https://docs.getgophish.com/))
	- **Campaign**: Campaña de phishing que se creara con *Users & Groups*, *Email Template*, *Sending Profiles* para ejecutar la mismal y hacer seguimiento de las métricas obtenidas a raiz de la misma.  
	- **Groups**: Lista de usuarios contra los que se buscará realizar la campaña.
	- **Email template**: Template utilizado por gopish para enviar en el mail (Preferiblemente `.html`).
		- [Variables](https://docs.getgophish.com/user-guide/template-reference): Este apartado cuenta con variables que se utilizarán y consumirán de la *lista de Groups* con el fin de "personalizar" cada email:
			- *{{.FirstName}}*: Nombre que aparece en la lista de groups.
			- *{{.LastName}}*: Apellido que aparece en la lista de groups.
			- *{{.URL}}*: URL para realizar phishing.
			- *{{Email}}*: Email del objetivo que aparece en la lista de groups
			- *{{Position}}*: Posición del objetivo. (Internamente utilizada para enviar el **SHA256** del *email* para trackear).
			- *{{.Tracker}}* o *\<img src="{{.TrackingURL}}"*
	- **Sending Profiles**: Cuenta/s de email utilizadas junto a su servidor **SMTP** para realizar el phishing.

- *Back* (Custom app):

Consume los recursos de `/campaings/{campaignName}/*.html` para renderizar los 

```bash
/custom_app
|__ campaigns/
|     |__ first_campaign/
|     |    |__ templates/
|     |    |     |__ malicious_login.html 
|     |    |     |__ malicious_login_success.html
|     |    |__ data/
|     |         |__ email_list_for_campaign.txt
|     |
|     |__ second_campaign/
|
|__ common_assets/
|	 |__ image_used_by_any_campaign.png
|	 |__ other_image_used.png
|
|__ config/
|	 |__ campaign_config.json
|
|__ logs/
|	 |__ logs_generateds.log
|
|__ main.py	 	
```

-----
# TODO

- Para la **aplicación**:
- [ ] Exportar archivo `.csv` subible en *Gopish*.
- [ ] Refactorizar y modularizar el código.
- [ ] Independizar configuraciones y assets de campañas.
- [ ] Agregar escenario "not found" para cualquier url que ingrese el usuario dentro de una campaña (Que redirijá al sitio oficial).

- Para los **procesos**:
- [ ] Mejorar la documentación interna.
- [ ] Realizar documentos explicativos sobre el proceso.