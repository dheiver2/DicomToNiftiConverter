
# Conversor DICOM para NIfTI com Agendamento Automático

Este projeto permite converter arquivos DICOM para o formato NIfTI, agendar a execução da tarefa diariamente ou executá-la imediatamente no Google Colab. Após a conversão, os arquivos NIfTI são enviados por e-mail.

## Funcionalidades

- **Conversão DICOM para NIfTI**: Converte arquivos DICOM localizados em uma pasta específica para o formato NIfTI.
- **Busca Automática de Arquivos Não Convertidos**: Identifica automaticamente os arquivos DICOM que ainda não foram convertidos.
- **Envio de Arquivos por E-mail**: Após a conversão, os arquivos NIfTI são enviados por e-mail como anexos.
- **Agendamento de Execução**:
  - **Diário**: Execute a tarefa automaticamente em horários específicos do dia.
  - **Execução Imediata**: Execute a tarefa manualmente ao rodar a célula no Google Colab.

## Pré-requisitos

1. **Google Colab**:
   - O código foi desenvolvido para ser executado no ambiente do Google Colab.
   - Certifique-se de ter acesso a uma conta Google.

2. **Dependências**:
   - As bibliotecas necessárias (`pydicom`, `nibabel`, `schedule`) serão instaladas automaticamente ao executar o código.

3. **Configuração de E-mail**:
   - Utilize um servidor SMTP (como Gmail) para enviar os arquivos por e-mail.
   - Configure as credenciais de e-mail no código (veja abaixo).

4. **Pastas de Entrada e Saída**:
   - Crie uma pasta para os arquivos DICOM de entrada (ex.: `/content/dicom_files`).
   - Crie uma pasta para os arquivos NIfTI de saída (ex.: `/content/nifti_files`).

## Como Usar

### 1. Configurar o Código

No início do código, configure as seguintes variáveis:

```python
input_folder = "/content/dicom_files"  # Pasta onde estão os arquivos DICOM
output_folder = "/content/nifti_files"  # Pasta onde os arquivos NIfTI serão salvos
email_config = {
    "smtp_server": "smtp.gmail.com",  # Servidor SMTP (ex.: Gmail)
    "port": 587,                      # Porta SMTP (ex.: 587 para Gmail)
    "sender_email": "seu_email@gmail.com",  # Seu e-mail
    "receiver_email": "destinatario@gmail.com",  # E-mail do destinatário
    "password": "sua_senha"           # Senha do seu e-mail (ou senha de app)
}
```

### 2. Carregar Arquivos DICOM

Carregue os arquivos DICOM para a pasta `/content/dicom_files` no Google Colab. Você pode fazer isso arrastando os arquivos para a interface do Colab ou usando o comando `!wget` para baixar arquivos de uma URL.

### 3. Executar o Código

#### Opção 1: Execução Imediata
Se você deseja executar a tarefa imediatamente ao rodar a célula, use o seguinte trecho de código:

```python
converter = DicomToNiftiConverter(input_folder, output_folder, email_config)
converter.process_files()
```

#### Opção 2: Agendamento Diário
Se você deseja agendar a execução da tarefa para horários específicos do dia, use o seguinte trecho de código:

```python
daily_times = ["09:00", "15:00", "21:00"]  # Horários de execução (formato HH:MM)
converter.schedule_daily_task(daily_times)
```

### 4. Verificar os Resultados

- Os arquivos NIfTI convertidos serão salvos na pasta `/content/nifti_files`.
- Os arquivos NIfTI também serão enviados por e-mail para o destinatário configurado.

## Observações Importantes

1. **Google Colab**:
   - O ambiente do Colab não mantém o código em execução indefinidamente. Para agendamentos contínuos, considere usar um serviço como AWS, GCP ou Heroku.

2. **Gmail**:
   - Para evitar problemas com o Gmail, habilite o acesso a aplicativos menos seguros ou configure uma [senha de app](https://support.google.com/accounts/answer/185833?hl=pt-BR).

3. **Fuso Horário**:
   - O Google Colab usa o fuso horário UTC por padrão. Certifique-se de ajustar os horários de agendamento conforme necessário.

4. **Erros Comuns**:
   - Certifique-se de que os arquivos DICOM estejam corretamente formatados.
   - Verifique se as pastas de entrada e saída existem antes de executar o código.

## Contribuições

Contribuições são bem-vindas! Se você encontrar bugs ou quiser melhorar o código, sinta-se à vontade para abrir uma issue ou enviar um pull request.

## Licença

Este projeto está licenciado sob a [MIT License](https://opensource.org/licenses/MIT).
