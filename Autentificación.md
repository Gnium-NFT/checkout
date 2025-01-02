Documentación de GitHub
Autenticación /Seguridad de la cuenta /Administrar tokens de acceso personal
Administrar sus tokens de acceso personales
Puede utilizar un token de acceso personal en lugar de una contraseña al autenticarse en GitHub en la línea de comando o con la API.

En este artículo
Acerca de los tokens de acceso personal
Creación de un token de acceso personal de granularidad fina
Creación de un token de acceso personal (clásico)
Eliminar un token de acceso personal
Uso de un token de acceso personal en la línea de comandos
Lectura adicional
Advertencia

Trate sus tokens de acceso como si fueran contraseñas. Para obtener más información, consulte Cómo mantener seguros sus tokens de acceso personales .

Acerca de los tokens de acceso personal
Los tokens de acceso personal son una alternativa al uso de contraseñas para la autenticación en GitHub cuando se utiliza la API de GitHub o la línea de comandos .

Los tokens de acceso personal están pensados ​​para acceder a los recursos de GitHub en su nombre. Para acceder a los recursos en nombre de una organización o para integraciones de larga duración, debe utilizar una aplicación de GitHub. Para obtener más información, consulte Acerca de la creación de aplicaciones de GitHub .

Un token tiene las mismas capacidades para acceder a los recursos y realizar acciones en ellos que el propietario del token, y está limitado además por los alcances o permisos otorgados al token. Un token no puede otorgar capacidades de acceso adicionales a un usuario. Por ejemplo, un token de acceso personal se puede configurar con un admin:orgalcance, pero si el propietario del token no es propietario de una organización, el token no otorgará acceso administrativo a la organización.

Tipos de tokens de acceso personal
GitHub actualmente admite dos tipos de tokens de acceso personal: tokens de acceso personal de granularidad fina y tokens de acceso personal (clásicos). GitHub recomienda que utilices tokens de acceso personal de granularidad fina en lugar de tokens de acceso personal (clásicos) siempre que sea posible.

Tanto los tokens de acceso personal de grano fino como los tokens de acceso personal (clásicos) están vinculados al usuario que los generó y se volverán inactivos si el usuario pierde el acceso al recurso.

Los propietarios de organizaciones pueden establecer una política para restringir el acceso de tokens de acceso personal (clásico) a su organización. Para obtener más información, consulte Establecer una política de tokens de acceso personal para su organización .

Tokens de acceso personal de grano fino
Los tokens de acceso personal de grano fino tienen varias ventajas de seguridad sobre los tokens de acceso personal (clásicos):

Cada token solo puede acceder a recursos propiedad de un solo usuario u organización.
Cada token solo puede acceder a repositorios específicos.
A cada token se le otorgan permisos específicos, que ofrecen más control que los alcances otorgados a los tokens de acceso personal (clásico).
Los propietarios de organizaciones pueden solicitar aprobación para cualquier token de acceso personal de grano fino que pueda acceder a los recursos de la organización.
Tokens de acceso personal (clásicos)
Los tokens de acceso personal (clásicos) son menos seguros. Sin embargo, algunas funciones actualmente solo funcionan con tokens de acceso personal (clásicos):

Solo los tokens de acceso personal (clásicos) tienen acceso de escritura a repositorios públicos que no son de su propiedad ni de una organización de la que no es miembro.
Los colaboradores externos solo pueden usar tokens de acceso personales (clásicos) para acceder a los repositorios de la organización en los que son colaboradores.
Algunos puntos finales de la API REST solo están disponibles con tokens de acceso personal (clásico). Para comprobar si un punto final también admite tokens de acceso personal de granularidad fina, consulte la documentación de ese punto final o consulte Puntos finales disponibles para tokens de acceso personal de granularidad fina .
Si elige utilizar un token de acceso personal (clásico), tenga en cuenta que le otorgará acceso a todos los repositorios dentro de las organizaciones a las que tenga acceso, así como a todos los repositorios personales en su cuenta personal.

Como medida de seguridad, GitHub elimina automáticamente los tokens de acceso personal que no se han utilizado durante un año. Para brindar mayor seguridad, recomendamos encarecidamente agregar una fecha de vencimiento a los tokens de acceso personal.

Cómo mantener seguros sus tokens de acceso personal
Los tokens de acceso personal son como contraseñas y comparten los mismos riesgos de seguridad inherentes. Antes de crear un nuevo token de acceso personal, considere si existe un método de autenticación más seguro disponible para usted:

Para acceder a GitHub desde la línea de comandos, puedes usar GitHub CLI o Git Credential Manager en lugar de crear un token de acceso personal.
Al utilizar un token de acceso personal en un flujo de trabajo de GitHub Actions, considere si puede utilizar el token integrado GITHUB_TOKENen su lugar. Para obtener más información, consulte Autenticación automática con token .
Si estas opciones no son posibles y debe crear un token de acceso personal, considere usar otro servicio CLI para almacenar su token de forma segura.

Al usar un token de acceso personal en un script, puedes almacenar tu token como un secreto y ejecutar tu script a través de GitHub Actions. Para obtener más información, consulta Usar secretos en GitHub Actions . También puedes almacenar tu token como un secreto de Codespaces y ejecutar tu script en Codespaces. Para obtener más información, consulta Administrar tus secretos específicos de la cuenta para GitHub Codespaces .

Para obtener más información sobre las mejores prácticas, consulte Cómo mantener seguras sus credenciales de API .

Creación de un token de acceso personal de granularidad fina
Nota

Los tokens de acceso personal de grano fino se encuentran actualmente en versión preliminar pública y están sujetos a cambios. Para dejar comentarios, consulte la discusión de comentarios .

Verifique su dirección de correo electrónico , si aún no ha sido verificada.

En la esquina superior derecha de cualquier página de GitHub, haz clic en tu foto de perfil y luego en Configuración .

En la barra lateral izquierda, haga clic en Configuración del desarrollador .

En la barra lateral izquierda, en Tokens de acceso personal , haga clic en Tokens de granularidad fina .

Haga clic en Generar nuevo token .

En Nombre del token , ingrese un nombre para el token.

En Vencimiento , seleccione un vencimiento para el token. Se permiten duraciones infinitas, pero pueden estar bloqueadas por una política de duración máxima establecida por su organización o el propietario de la empresa. Para obtener más información, consulte Aplicación de una política de duración máxima para tokens de acceso personal .

Opcionalmente, en Descripción , agregue una nota para describir el propósito del token.

En Propietario del recurso , seleccione un propietario del recurso. El token solo podrá acceder a los recursos que sean propiedad del propietario del recurso seleccionado. Las organizaciones de las que usted es miembro no aparecerán a menos que la organización haya optado por usar tokens de acceso personal específicos. Para obtener más información, consulte Establecer una política de token de acceso personal para su organización .

De manera opcional, si el propietario del recurso es una organización que requiere aprobación para tokens de acceso personal específicos, debajo del propietario del recurso, en el cuadro, ingrese una justificación para la solicitud.

En Acceso al repositorio , selecciona los repositorios a los que deseas que acceda el token. Debes elegir el acceso mínimo al repositorio que se ajuste a tus necesidades. Los tokens siempre incluyen acceso de solo lectura a todos los repositorios públicos de GitHub.

Si seleccionó Seleccionar solo repositorios en el paso anterior, en el menú desplegable Repositorios seleccionados , seleccione los repositorios a los que desea que acceda el token.

En Permisos , seleccione qué permisos otorgar al token. Según el propietario del recurso y el acceso al repositorio que haya especificado, existen permisos de repositorio, de organización y de cuenta. Debe elegir los permisos mínimos necesarios para sus necesidades.

El documento de referencia de la API REST para cada punto final indica si el punto final funciona con tokens de acceso personal de grano fino y qué permisos se requieren para que el token utilice el punto final. Algunos puntos finales pueden requerir varios permisos y otros pueden requerir uno de varios permisos. Para obtener una descripción general de los puntos finales de la API REST a los que puede acceder un token de acceso personal de grano fino con cada permiso, consulte Permisos necesarios para tokens de acceso personal de grano fino .

Haga clic en Generar token .

Si seleccionó una organización como propietaria del recurso y la organización requiere aprobación para tokens de acceso personal específicos, su token se marcará como tal pendinghasta que lo revise un administrador de la organización. Su token solo podrá leer recursos públicos hasta que se apruebe. Si es propietario de la organización, su solicitud se aprueba automáticamente. Para obtener más información, consulte Revisión y revocación de tokens de acceso personal en su organización .

Creación de un token de acceso personal (clásico)
Nota

Los propietarios de organizaciones pueden restringir el acceso del token de acceso personal (clásico) a su organización. Si intenta utilizar un token de acceso personal (clásico) para acceder a los recursos de una organización que ha deshabilitado el acceso al token de acceso personal (clásico), su solicitud fallará con una respuesta 403. En su lugar, debe utilizar una aplicación de GitHub, una aplicación de OAuth o un token de acceso personal específico.

Advertencia

Tu token de acceso personal (clásico) puede acceder a todos los repositorios a los que puedas acceder. GitHub recomienda que utilices tokens de acceso personal de granularidad fina, que puedes restringir a repositorios específicos. Los tokens de acceso personal de granularidad fina también te permiten especificar permisos de granularidad fina en lugar de alcances amplios.

Verifique su dirección de correo electrónico , si aún no ha sido verificada.

En la esquina superior derecha de cualquier página de GitHub, haz clic en tu foto de perfil y luego en Configuración .

En la barra lateral izquierda, haga clic en Configuración del desarrollador .

En la barra lateral izquierda, en Tokens de acceso personal , haga clic en Tokens (clásico) .

Seleccione Generar nuevo token y luego haga clic en Generar nuevo token (clásico) .

En el campo "Nota", dale un nombre descriptivo a tu token.

Para darle una fecha de vencimiento a su token, seleccione Vencimiento , luego elija una opción predeterminada o haga clic en Personalizado para ingresar una fecha.

Seleccione los ámbitos que desea otorgar a este token. Para usar su token para acceder a repositorios desde la línea de comandos, seleccione repo . Un token sin ámbitos asignados solo puede acceder a información pública. Para obtener más información, consulte Ámbitos para aplicaciones OAuth .

Haga clic en Generar token .

Opcionalmente, para copiar el nuevo token a su portapapeles, haga clic en .

Captura de pantalla de la página "Tokens de acceso personal". Junto a un token borroso, se muestra un icono de dos cuadrados superpuestos delineados en naranja.
Para usar su token para acceder a recursos que son propiedad de una organización que utiliza el inicio de sesión único SAML, autorice el token. Para obtener más información, consulte Autorización de un token de acceso personal para su uso con el inicio de sesión único SAML en la documentación de GitHub Enterprise Cloud.

Eliminar un token de acceso personal
Debes eliminar un token de acceso personal si ya no lo necesitas. Si eliminas un token de acceso personal que se utilizó para crear una clave de implementación, la clave de implementación también se eliminará.

En la esquina superior derecha de cualquier página de GitHub, haz clic en tu foto de perfil y luego en Configuración .
En la barra lateral izquierda, haga clic en Configuración del desarrollador .
En la barra lateral izquierda, en Tokens de acceso personal , haga clic en Tokens de grano fino o Tokens (clásicos) , según el tipo de token de acceso personal que desee eliminar.
A la derecha del token de acceso personal que desea eliminar, haga clic en Eliminar .
Uso de un token de acceso personal en la línea de comandos
Una vez que tenga un token de acceso personal, puede ingresarlo en lugar de su contraseña al realizar operaciones de Git a través de HTTPS.

Por ejemplo, para clonar un repositorio en la línea de comandos, debe ingresar el siguiente git clonecomando. Luego, se le solicitará que ingrese su nombre de usuario y contraseña. Cuando se le solicite su contraseña, ingrese su token de acceso personal en lugar de una contraseña.

$ git clone https://github.com/USERNAME/REPO.git
Username: YOUR-USERNAME
Password: YOUR-PERSONAL-ACCESS-TOKEN
Los tokens de acceso personal solo se pueden usar para operaciones Git HTTPS. Si su repositorio usa una URL remota SSH, deberá cambiar el control remoto de SSH a HTTPS .

Si no se le solicita su nombre de usuario y contraseña, es posible que sus credenciales estén almacenadas en caché en su computadora. Puede actualizar sus credenciales en el llavero para reemplazar su contraseña anterior con el token.

En lugar de ingresar manualmente su token de acceso personal para cada operación HTTPS de Git, puede almacenar en caché su token de acceso personal con un cliente de Git. Git almacenará temporalmente sus credenciales en la memoria hasta que transcurra un intervalo de vencimiento. También puede almacenar el token en un archivo de texto sin formato que Git pueda leer antes de cada solicitud. Para obtener más información, consulte Almacenamiento en caché de sus credenciales de GitHub en Git .

Lectura adicional
Acerca de la autenticación en GitHub
Caducidad y revocación de tokens
