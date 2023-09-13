import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from email.mime.image import MIMEImage




class sendemail:
    msgcorpohtml = """ 
                     <html>
                        <head></head>
                            <body>
                            <p>Estimado Cliente,<br><br>
    
                    
                    estamos a trabalhar para executarmos a sua transferência internacional, com o máximo de brevidade possível. <br><br>

                    Agradecemos a sua preferência e compreensão.<br>
                    <b>BANCO MILLENNIUM ATLANTICO</b> <br><br><br>
                    <img src="cid:image1" alt="rodapé"> <br>
                    Nota: Este e-mail é gerado automaticamente.
                     </p>
  </body>
</html>
 """

    image = MIMEImage(open('rodapeatl.png', 'rb').read())
    image.add_header('Content-ID','<image1>')

    def sendemailf(email, corpo, psubject, psender,image1):

        address_book = [email]
        cc = ['josemar.costa.manuel@atlantico.ao']
        msg = MIMEMultipart()    
        sender = 'dbi.automacao.processos@atlantico.ao'
        subject = psubject
        body = corpo

        msg['From'] = psender
        msg['To'] = ','.join(address_book)
        msg['Subject'] = subject
        
        msg.attach(image1)
        msg.attach(MIMEText(body, 'html'))
        text=msg.as_string()
        #print text
        #Send the message via our SMTP server

        


        s = smtplib.SMTP('smtp.atlantico.int',25)
        s.sendmail(sender,address_book, text)
        s.quit()
        #msgcorpohtml    

    sendemailf('edmundovalente18@gmail.com',msgcorpohtml,'Notificação 5 dias','Ope.notificacao@atlantico.ao',image) 