<img src="./img/logo.png" alt="Chmurowisko logo" width="200" align="right">
<br><br>
<br><br>
<br><br>

# Logowanie do maszyny studenckiej za pomocą SSH

W tym laboratorium dowiesz się jak zalogować się na maszynę VM podczas ćwiczeń związanych z Docker oraz jak zainstalować samego Dockera.

---

## Krok 1: Logowanie do maszyny studenckiej

1. Przejdź do [portal.azure.com](https://portal.azure.com) i uruchom Cloud Shell.
1. W Cloud Shell wykonaj ponizszą komendę i skopiuj adres IP dla swojej maszyny (z numerem Twojego konta studenta)

    ```bash
    az vm list-ip-addresses --query "[].{name:virtualMachine.name, IP:virtualMachine.network.publicIpAddresses[0].ipAddress}" -o table
    ```

1. Uzupełnij ponizszą komendę swoim loginem studenta oraz skopiowanym adresem IP i wykonaj ją w Cloud Shell

    ```bash
    ssh <login>@<vm-ip>
    ```

    Gotowa komenda powinna wyglądać podobnie do tej:

    ```bash
    ssh cmst01@20.100.200.10
    ```

1. Zapytany o autentyczność hosta wpisz `yes` i naciśnij Enter

    ```bash
    The authenticity of host '20.100.200.10 (20.100.200.10)' can't be established.
    ECDSA key fingerprint is SHA256:l9i...WTe7FPg...IDGQw/ZFJt...AB60.
    Are you sure you want to continue connecting (yes/no)?
    ```

1. W tym kroku podasz hasło uzytkownika. Kazdy uzytkownik posiada haslo w formacie:

    ```bash
    VMstudentXX!
    ```

    gdzie `XX` to Twój numer studenta

    Przykładowe hasło uzytkownika o loginie `cmst01` to `VMstudent01!`

    Po wpisaniu hasła zatwierdź próbę logowania naciskając Enter.

1. Powinieneś zostać zalogowany z sukcesem.

---

## Krok 2: Instalacja Docker na maszynie studenckiej

> Dokładny opis kroków instalacji mozesz znaleźć na stronie: https://docs.docker.com/engine/install/ubuntu/

1. Wykonaj ponizsze komendy

    ```bash
    sudo apt-get update
    ```

    ```bash
    sudo apt-get install \
        apt-transport-https \
        ca-certificates \
        curl \
        gnupg \
        lsb-release
    ```

    Potwierdź chęć instalacji naciskając `Y`.

    ```bash
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
    ```

    ```bash
    echo \
    "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    ```

    ```bash
    sudo apt-get update
    ```

    ```bash
    sudo apt-get install docker-ce docker-ce-cli containerd.io
    ```

    Potwierdź chęć instalacji naciskając `Y`.

1. Zaloguj się na `su`

    ```bash
    sudo su -
    ```

1. Sprawdź czy Docker został poprawnie zainstalowany

    ```bash
    docker run hello-world
    ```

---

## END LAB

<br><br>

<center><p>&copy; 2021 Chmurowisko Sp. z o.o.<p></center>
