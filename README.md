# Isa Rossi — Sistema de agendamento

## Páginas
- `index.html`: site público.
- `agendar.html`: reservas das clientes, datas e horários disponíveis em tempo real no banco.
- `admin.html`: login restrito, dashboard, agenda por dia/semana/mês, edição, cancelamentos, serviços e horários.
- `styles-app.css`: identidade visual dos aplicativos.
- `config.js`: URL + **chave publicável** do Supabase.
- `supabase-setup.sql`: tabelas, políticas de acesso e funções de agendamento.

## Ativação
1. Criar projeto Supabase **exclusivo** para a Isa; não use outro projeto de cliente.
2. Executar `supabase-setup.sql` no SQL Editor do projeto.
3. Copiar a Project URL e publishable key em `config.js`. **Nunca colocar secret/service_role no repositório.**
4. Em Authentication, criar uma conta da administradora com email e senha seguros, confirmar o email e copiar o UID desse usuário.
5. No SQL Editor, executar: `insert into public.isa_admins(user_id) values ('UUID-DA-ADMINISTRADORA');`
6. Em Authentication > URL Configuration, adicionar a URL publicada do GitHub Pages à lista de redirect URLs se usar recuperação de senha. Para a versão atual, o login utiliza email e senha.
7. Em GitHub Settings > Pages > Build and deployment, usar branch `main` e pasta `/(root)`.
8. Testar uma solicitação em janela anônima e conferir que aparece no dashboard, que o horário deixa de estar disponível e que outro visitante não consegue ver dados de clientes.

## Operação
- Clientes não criam login. Fazem solicitação, inicialmente como **Aguardando**.
- A administradora confirma, conclui, cancela ou marca ausência.
- Cancelamentos liberam horários. Pendentes, confirmados e concluídos bloqueiam conflitos.
- O banco impede sobreposição também sob reservas simultâneas.
- Horários de funcionamento iniciais são **apenas exemplo**; configure horários reais no painel.
- O preço inicial é desconhecido e deve ser definido pela profissional. Receita no painel soma valores de atendimentos concluídos com preço cadastrado; não representa pagamentos conciliados.
- Registros podem conter dados pessoais: obtenha consentimento adequado e estabeleça política de privacidade, retenção e atendimento à LGPD antes de uso real.
- Configurar proteção anti-spam/CAPTCHA e limitação de tentativas via backend antes da abertura pública ampla; a versão inicial não inclui isso.
- Alterações no horário de funcionamento não cancelam reservas já existentes.
- O navegador usa America/Sao_Paulo como referência de exibição. Para fusos diferentes, adaptar conversão manual do painel.
- **Importante:** até conectar um Supabase, páginas exibem aviso e não registram agendamentos. GitHub Pages sozinho não armazena reservas compartilhadas.
