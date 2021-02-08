# Cheat sheet

Use this file to write down the most important commands you encounter, so you can look them up quickly. Put some clear structure in this document, or split it up if it becomes too large. [Use Markdown correctly](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/). For inspiration and a motivation for why you should keep this type of cheat sheets, take a look at <https://github.com/bertvv/cheat-sheets/>.

## Vim survival guide

- When starting up Vim, you're in *normal mode*.
- To enter text, first go to *insert mode*.

| Taak                       | Commando |
| :---                       | :---     |
| Normal mode -> insert mode | `i`      |
| Insert mode -> normal mode | `<Esc>`  |
| Opslaan                    | `:w`     |
| Opslaan en afsluiten       | `:wq`    |
| Afsluiten zonder opslaan   | `:q!`    |

## Firewall commandos

- Firewall starten: `sudo systemctl start firewalld`
- Zone toevoegen: `sudo firewall-cmd --add-service=http --zone=public `
- Firewall zones controleren: `firewall-cmd --list-all`
- firewall port toevoegen: `sudo firewall-cmd --zone=public --permanent --add-port=5000/tcp`


## Ports
- Listening ports: ss -tlnp : lists ports and processes

## Logs
- Journalctl -f : Live logs 
