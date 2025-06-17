Automação de Cadastro de Avaliação - SAC CEDAE
Este projeto automatiza o preenchimento de formulários de avaliação de atendimento do SAC da CEDAE. A ferramenta foi desenvolvida para solucionar um problema crítico que surgiu durante a manutenção do sistema de automação da empresa de Call Center parceira.

Nesse período, para que os registros não fossem perdidos, todas as avaliações de atendimento passaram a ser exportadas para planilhas Excel (.xlsx). Isso gerou a necessidade de um registro manual dos dados no sistema interno da CEDAE — um processo lento, repetitivo e sujeito a erros.

Este script elimina completamente essa tarefa manual. Ele lê os dados diretamente da planilha e os insere na página web, garantindo a integridade dos registros e otimizando drasticamente o tempo da equipe.

✨ Funcionalidades
Leitura de Dados: Extrai informações de planilhas Excel (.xlsx) de forma automática.
Automação Web: Utiliza Selenium para navegar e preencher formulários em uma página web.
Processamento em Lote: Cadastra múltiplas avaliações em sequência, uma para cada linha da planilha.
Feedback de Execução: Exibe no console o status de envio de cada formulário, informando sucessos e erros.
🔧 Pré-requisitos
Antes de executar o script, garanta que você tenha o seguinte instalado:

Python 3
Google Chrome (Navegador)
ChromeDriver: O driver precisa ser compatível com a sua versão do Google Chrome. A versão utilizada durante o desenvolvimento foi a 131.0.6778.204. Você pode baixar a versão correta no site oficial do Chrome for Testing.
Acesso à rede interna da CEDAE, pois o script acessa um endereço local (https://10.10.35.17).
selenium 4.27.1
pandas 2.2.3
openpyxl 3.1.5

⚙️ Exemplo de uso caso fossemos usar o código no servidor da CEDAE.
Clone o repositório:

Bash

git clone https://github.com/joaofroez/nome-do-repositorio.git
cd nome-do-repositorio
Crie um ambiente virtual (recomendado):

Bash

python -m venv venv
No Windows, ative com: .\venv\Scripts\activate
No macOS/Linux, ative com: source venv/bin/activate
Instale as dependências a partir do arquivo requirements.txt:

Bash

pip install -r requirements.txt
Se você não tiver um arquivo requirements.txt, crie um com o seguinte conteúdo:

pandas==2.2.3
selenium==4.27.1
openpyxl==3.1.5
Configure o ChromeDriver:

Baixe o ChromeDriver compatível com sua versão do Chrome.
Coloque o arquivo executável (chromedriver.exe no Windows) na mesma pasta do script cadastro_avaliacao.py ou em um diretório que esteja no PATH do seu sistema.
▶️ Como Usar
Prepare sua planilha:

Crie um arquivo Excel com o nome NumerosPesquisaSAC_Ausentes_08012025.xlsx (ou altere o nome do arquivo no final do script cadastro_avaliacao.py).
A planilha deve conter as seguintes colunas: Data_fim, Avaliado, e Numero (Avaliador).
Exemplo da estrutura da planilha:

Data_fim	Avaliado	Numero (Avaliador)
1673182800	21987654321	1001
1673183100	21912345678	1002

Exportar para as Planilhas
Execute o script:

Certifique-se de que você está conectado à rede da CEDAE.
Abra o terminal, navegue até a pasta do projeto e execute o comando:
<!-- end list -->

Bash

python cadastro_avaliacao.py
Acompanhe o processo:

O script abrirá uma janela do Chrome e começará a preencher os formulários. Você verá mensagens de status no terminal para cada registro processado.
📝 Configuração e Personalização
O script pode ser facilmente adaptado para diferentes necessidades:

Arquivo de Entrada: Para usar um arquivo Excel com outro nome, altere a variável arquivo_excel no final do script:

Python

# Caminho do arquivo Excel
arquivo_excel = "outro_arquivo.xlsx"
Valores Fixos no Formulário: Os valores para as perguntas (p1, p2, p3) e o tipo da avaliação estão definidos como fixos no código. Para alterá-los, modifique o dicionário dados_formulario dentro da função processar_planilha_e_preencher_formulario:

Python

dados_formulario = {
    # ... outros campos
    "p1": "10",
    "p2": "10",
    "p3": "10",
    "tipo": "REALIZADA"
}
⚠️ Observações Importantes
Rede Interna: Este script foi projetado para acessar um sistema no endereço https://10.10.35.17, que só é acessível pela rede interna da CEDAE.
Certificado SSL: A automação está configurada para ignorar erros de certificado SSL (--ignore-certificate-errors), uma prática comum para acessar sistemas internos de desenvolvimento ou homologação que não possuem um certificado público válido.
