# MGCEP

[![License](https://img.shields.io/badge/license-PolyForm%20Perimeter%201.0.1-5351FB)](LICENSE.md)

É uma biblioteca **leve e simples em PHP** para consulta de CEP utilizando a API pública do **ViaCEP**, com suporte a **cache local em arquivos** para melhorar desempenho e reduzir requisições externas.

Ideal para aplicações que precisam de **consultas rápidas de endereço**, com **baixo consumo de recursos** e **fácil integração**.

---

## ✨ Características

* Consulta de CEP via **ViaCEP**
* Cache local em arquivos (`.json`)
* Configuração de tempo de cache (TTL)
* API simples e direta
* Zero dependências externas
* Compatível com **PHP 8+**

---

## 📦 Instalação

### Manual

Copie a classe `MGCEP.php` para seu projeto e utilize via `require` ou autoload:

```php
composer require profmugomes/mgcep;
```

---

## ⚙️ Configuração

Antes de utilizar, é recomendado configurar o diretório de cache:

```php
use MGCEP\MGCEP;

$cep = new MGCEP();
$cep->setCacheDir(__DIR__ . '/cache');
```

---

## 📮 Consulta de CEP

```php
$erro = $cep->getCEP('01001000');

if ($erro) {
    echo $erro;
} else {
    echo $cep->getLogradouro();
}
```

---

## 🧠 Métodos Públicos

### 📁 setCacheDir

Define o diretório onde os arquivos de cache serão armazenados.

```php
$cep->setCacheDir('/caminho/do/cache');
```

**Parâmetros:**

* `string $path` → Caminho do diretório
* `int $permission` → Permissão (padrão: `0777`)

---

### ⏱️ setCacheTTL

Define o tempo de vida do cache em segundos.

```php
$cep->setCacheTTL(3600); // 1 hora
```

---

### 🔍 getCEP

Realiza a consulta do CEP.

```php
$erro = $cep->getCEP('01001000');
```

**Retorno:**

* `false` → Sucesso
* `string` → Mensagem de erro

---

## 📍 Métodos de Dados

Após uma consulta bem-sucedida (`getCEP`), os dados podem ser acessados:

---

### 🏠 Endereço

```php
$cep->getLogradouro();
$cep->getComplemento();
$cep->getUnidade();
$cep->getBairro();
```

---

### 🌆 Localização

```php
$cep->getLocalidade();
$cep->getUF();
$cep->getEstado();
$cep->getRegiao();
```

---

### 🏛️ Informações adicionais

```php
$cep->getIBGE();
$cep->getGIA();
$cep->getDDD();
$cep->getSIAFI();
```

---

## 💡 Exemplo completo

```php
use MGCEP\MGCEP;

$cep = new MGCEP();
$cep->setCacheDir(__DIR__ . '/cache');
$cep->setCacheTTL(86400); // 1 dia

$erro = $cep->getCEP('01001000');

if ($erro) {
    echo "Erro: $erro";
    exit;
}

echo 'Rua: ' . $cep->getLogradouro() . PHP_EOL;
echo 'Bairro: ' . $cep->getBairro() . PHP_EOL;
echo 'Cidade: ' . $cep->getLocalidade() . PHP_EOL;
echo 'UF: ' . $cep->getUF() . PHP_EOL;
```

---

## ⚠️ Observações

* É necessário chamar `getCEP()` antes de acessar os métodos de dados
* O cache é baseado no **hash da URL**
* Arquivos expirados são removidos automaticamente
* Requer conexão com internet na primeira consulta

---

## 👤 Autor

**Murilo Gomes**

🔗 [https://www.profmugomes.com.br](https://www.profmugomes.com.br)

📺 [https://youtube.com/@profmugomes](https://youtube.com/@profmugomes)

---

## 🤝 Support

* GitHub Sponsors: [https://github.com/sponsors/profmugomes](https://github.com/sponsors/profmugomes)

## License

Copyright (c) 2026 Murilo Gomes <profmugomes.com.br>. All Rights Reserved.

This project is licensed under the PolyForm Perimeter License 1.0.1.

### Summary

This software is available for commercial and noncommercial use, subject to the terms of the PolyForm Perimeter License 1.0.1.

You may:

* ✔ Use the software for commercial and noncommercial purposes.
* ✔ Inspect and study the source code.
* ✔ Modify the software.
* ✔ Create derivative works based on the software.
* ✔ Redistribute the software and permitted modifications.

You may not:

* ✖ Provide a product that competes with the software.

See the full license terms at LICENSE.md.

This summary is provided for convenience only and does not replace or modify the full license terms.