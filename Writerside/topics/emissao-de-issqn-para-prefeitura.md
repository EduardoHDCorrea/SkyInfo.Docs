# Declaração de ISSQN para Prefeitura

<secondary-label ref="referencial-técnico"/>
<secondary-label ref="backend"/>

Projeto criado para testar a utilização da biblioteca ACBrLib, que é uma biblioteca de código aberto para a geração de arquivos de Nota Fiscal Eletrônica de Serviços (NFSe).

### Justificativa

Foi levantada a necessidade de emitir notas fiscais para a prefeitura de **Gramado**, portanto se decidiu desenvolver uma solução que possibilite a prestação de contas para diminuir o custo de implementação para qualquer cliente que surgir com a mesma necessidade.

Após falhas na utilização da biblioteca da `Tecnospeed`, e `OpenAC.NET`, foi decidido testar a utilização da biblioteca da `ACBr`.

---

## Detalhes Técnicos

- **Framework:** .NET 8.0
- **Sistema Operacional:** Linux x64 | Windows x64
- **Tipo:** Aplicação de Console
- **Ponto de Entrada:** Program.cs
- **Pacotes Nuget:**
    - [ACBrLib.Core 1.2.10](https://www.nuget.org/packages/ACBrLib.Core)
    - [ACBrLib.NFSe 1.0.3](https://www.nuget.org/packages/ACBrLib.NFSe)
    - [ini-parser-netstandard 2.5.2](https://www.nuget.org/packages/ini-parser-netstandard)
    - ... _(Outros pacotes da Sky/Microsoft)_

### Dependências da ACBrLib - Linux

A ACBrLib necessita que os seguintes estejam instalados para funcionar corretamente no Linux, além de precisar de um link simbólico para o arquivo `libxml2.so.2`:

```
  xvfb
  xauth
  openssl
  libxml2
  libgtk2.0-0
  ttf-mscorefonts-installer
```

O comando de exemplo disponibilizado pela ACBrLib é o seguinte:
```bash
  sudo apt-get install -y --no-install-recommends \
  
  xvfb \
  
  xauth \
  
  openssl \    
  
  libxml2 \
  
  libgtk2.0-0 \
  
  ttf-mscorefonts-installer && \
  
  ln -s libxml2.so.2 libxml2.so
```

Também é necessário mover o arquivo `libacbrnfse64.so` para o diretório `/usr/lib/`.

Fonte: [](https://acbr.sourceforge.io/ACBrLib/ComoInstalarDistribuir.html)
