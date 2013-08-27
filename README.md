jBossAS7SSLSetup
================

jBoss AS7 SSL Certificate Install and Configuration


jBoss AS 7 Server' a SSL sertifikası yüklemek için izlenecek yol. Türkçe kaynak eksikliğini gidermesi için buraya ekliyorum. 


1-	Başlat/Çalıştır/cmd.exe ( administrator olarak çalıştır. )
	
2-	cd C:\Program Files\Java\jre7\bin   ( Dizinine gir )

3-	KeyStore dosyası oluşturmak için consol ekranına aşağıdaki komutları yaz..
	
	-	C:\Program Files\Java\jre7\bin\keytool -genkey -alias yusufyilman -keyalg RSA -keystore yilman.keystore
		Enter keystore password: secret
		Re-enter new password: secret

		What is your first and last name?
			[Unknown]:  www.yusufyilman.com
		
		What is the name of your organizational unit?
			[Unknown]:  SOFTWARE DEVELOPER
		
		What is the name of your organization?
			[Unknown]:  Yusuf YILMAN
		  
		What is the name of your City or Locality?
			[Unknown]:  Istanbul
		  
		What is the name of your State or Province?
			[Unknown]:  Istanbul
		  
		What is the two-letter country code for this unit?
			[Unknown]:  TR
		  
		Is CN=www.yusufyilman.com, OU=SOFTWARE DEVELOPER, O=Yusuf YILMAN, L=Istanbul, ST=Istanbul, C=TR correct?
			[no]:  yes

			Enter key password for <deva>: secret
				(RETURN if same as keystore password):  
			Re-enter new password: secret
			
			
4-	CSR Dosyası Oluşturma : Keytool dosyasından SSL Firmasına göndermek üzere oluşturulan CSR metinini oluşturmak.
	-	C:\Program Files\Java\jre7\bin\keytool -certreq -keyalg RSA -file certreq.csr -keystore yilman.keystore
		Enter keystore password: secret
		You will need the text from this CSR when requesting a certificate.
		
	Örnek :
				-----BEGIN NEW CERTIFICATE REQUEST-----
		MIwgaMxCzAJBgNVBAYTAlRSMREwDwYDVQQIEwhJU1RBTkJVTDERMA8GA1UEBxMIIDGTCCAgECAQA
		SVNUQU5CVUwxOTA3BgNVBAoTMEdFUkNFSyBJVEhBTEFUIElIUkFDQVQgUEFaQVJMQU1BIHZlIFRJ
		Q0FSRVQgQS5TLjEQMA4GA1UECxMHSVRIQUxBVDEhMB8GA1UEAxMYd3d3LmdlcmNla2l0aGFsYXQu
		Y29tLnRyMIIBIjAOCAQ8AMIIBCgKCAQEAq+Lrn3QBsx2cvh5AiPy23bLYNBgkqhkiG9w0BAQEFAA
		T3rBgQYg3YYPoRo4R9AiDuSyQnqXQjslk51Gn3lUgbX9pzo+jAvlxUR6souti01RQHooysdOldy5
		seNr5shHvCuIIgj0CZh3N47HZELU3uPYNK3Tcfnxr6wNw66oKDax8hwn9qWX1WcnDax8hwn9qWX1
		tlZIcFSUqZMTVVhhF3bGmmnHE8dLDFIT97o99M2kL+5A1kic0v3htFX2oV0Lnr1YX9IV4pSGeImo
		6pS+/xO1WyKYekjHkLG/9ETYTCX6UPvvLhbUXKtC1idULT8YifGnTN1OtOe/gCrk+AkVGUsP9u73
		EvbFQ8hKncO2IQIDAQABoDAwLgYJKoZIhvcNAQkOMSEwHzAdBgNVHQ4EFgQU/o9kjWZU2x4Ih02w
		c0jgKINFCKEwDQYJKoZIABLf2g/vsLvzICOofksRDXE57EzCzl6AWIoIPe1HhvcNAQELBQADggEB
		Pw4nH7c8gle4cFgiy1DdQo+4Pjwo2XWvv4vCPLuC4q0ZjG084OCbJuMGmzBeesvk9BJBpyVW0a1e
		Nq7z38i37m4Fhpf/nkaA6VSQXQI7w54HbVyiYrcSFrhEiR1HPia5H3TgTzInBRKaO8Cj1xE0DjiD
		P+NaOSxSGowcPDjqtSS0qZIwBpg1YLHD/7BxAlNyaAnYoloGe8rLBLVUW0mpOnsOyAO2aD1RBrEX
		kGpRE0j+JadH+vldSWaFMxQRLcMqZLlCawEjJ6AZ7MpvisUdd8J+aari8HoQ4y7B57MI1gJEPTI=
		-----END NEW CERTIFICATE REQUEST-----

5-  SSL Firmasına 4. Adımda oluşturulan dosyanın içerisindeki yukarıdaki kodu gönderiyoruz. Bizden site ve site admini hakkında email adresi adres 
	vs gibi bilgiler istiyor. Mail adresimize daha sonra sertifkanın dosyalarını gönderiyor. COMODO Free de Toplamda 5 tane sertifika dosyası geliyor. 
	Bu sayı başka firma yada versiyonlarda değişiklik gösterebilir. admin@yusufyilman.com mail adresine sertifika geliyor.
	
6-	Gelen sertifikaları ilk oluşturduğumuz keystore dosyası içerisinde topluyoruz... Bu işlemde kullanılacak sertifikalar ve yüklenme sıraları Sertifika türüne 
	yada firmaya göre değişiklik gösterebilir. Ben Örneği COMODO Free SSL için yapıyorum.
		
	a-	Root Sertifikasını Yüklenmesi : alias olarak sertifika adını veriyoruz.
		C:\Program Files\Java\jre7\bin\keytool -import -trustcacerts -alias AddTrustExternalCARoot -file AddTrustExternalCARoot.crt -keystore yilman.keystore
			Enter keystore password: secret
			Sertifika eklendi.
			
	b-	Intermediate 1 Sertifikalarının Yüklenmesi : alias olarak sertifika adını veriyoruz.
		C:\Program Files\Java\jre7\bin\keytool -import -trustcacerts -alias UTNAddTrustSGCCA -file UTNAddTrustSGCCA.crt -keystore yilman.keystore
	  		Enter keystore password: secret
			Sertifika eklendi.
			
	c-	Intermediate 2 Sertifikalarının Yüklenmesi : alias olarak sertifika adını veriyoruz.
		C:\Program Files\Java\jre7\bin\keytool -import -trustcacerts -alias ComodoUTNSGCCA -file ComodoUTNSGCCA.crt -keystore yilman.keystore
	  		Enter keystore password: secret
			Sertifika eklendi.
			
	d-	Intermediate 3 Sertifikalarının Yüklenmesi : alias olarak sertifika adını veriyoruz.
		C:\Program Files\Java\jre7\bin\keytool -import -trustcacerts -alias EssentialSSLCA_2 -file EssentialSSLCA_2.crt -keystore yilman.keystore
	  		Enter keystore password: secret
			Sertifika eklendi.
			
	e-	Intermediate 3 Sertifikalarının Yüklenmesi : alias olarak ilk oluşturduğumuz keystore dosyasıda kullandığımız alias' ı veriyoruz. 
		C:\Program Files\Java\jre7\bin\keytool -import -trustcacerts -alias yusufyilman -file www_yusufyilman_com.crt -keystore yilman.keystore
	  		Enter keystore password: secret
			Sertifikaların yüklenmesi tamamlandı.
		
7-	JBoss AS7 Configurations : Oluşturulan keystore dosyasına yüklenmiş sertifikayı kullanabilmek için; bu adımda jBoss ' ta aşağıdaki gibi bazı ayarların yapılması gerekiyor.
	
	a-	Standalone.xml : Connector'ü düzenle.
	
		<subsystem xmlns="urn:jboss:domain:web:1.1" default-virtual-server="default-host" native="false">
			<connector name="http" protocol="HTTP/1.1" scheme="http" socket-binding="http"/>
			<connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" enable-lookups="false" secure="true">
				<ssl name="ssl" key-alias="yusufyilman" password="secret" certificate-key-file="../standalone/configuration/yilman.keystore" protocol="TLSv1"/>
			</connector>		
			<virtual-server name="default-host" enable-welcome-root="false">
				<alias name="localhost"/>
			</virtual-server>
		</subsystem>
	
	b-	Standalone.xml : Port ları düzenle.
		
		<socket-binding-group name="standard-sockets" default-interface="public" ...>
		<socket-binding name="http" port="80" />
		<socket-binding name="https" port="443" />
		...
		</socket-binding-group>
