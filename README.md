# Programando para a impressora LB-1000.

A LB-1000 possui modelos que se adequam às necessidades dos clientes, sendo o modelo LB-1000 Basic com interfaces USB e Serial e o modelo LB-1000 Advanced que além das interfaces USB e Serial, utiliza também interfaces Paralela e Ethernet. Além disso, a LB-1000 pode ser utilizada para impressão de etiquetas de 25,4 a 118mm de largura, em papel contínuo / recibo, etiqueta corte-vinco, com marca preta, perfurada ou formulário/sanfonada.

Para a manutenção do seu equipamento, especificações técnicas e visão de modo geral, pode ser visto o site http://www.bematech.com.br/administrador/files/equipamento/suporte/15/1418149563-Manual_Usuario_LB-1000_Portugues.pdf que contem o manual da impressora mais atual, nele vamos verificar a questão de descrição geral do produto, uma visão do produto e a estrutura física da LB 1000. Para a manutenção de como trocar de fita de impressão ou trabalhar com ela na versão térmica, pode ser vista também no manual.

Para o manual de programação pode ser visualizado o site http://www.bematech.com.br/administrador/files/equipamento/suporte/15/1394308827-Impressora%20de%20Etiquetas_LB-1000_Manual_05_Manual_Programacao_LB-1000.pdf que contem as especificações técnicas par a programação. Se precisar de um manual sobre as funções que a dll disponibiliza, clique aqui e baixe o manual técnico de programação das funções.

Confira alguns vídeos que mostram detalhes da impressora:
- http://youtu.be/dECMVuBxgJA - Instalação da LB-1000 para emular linguagens de comunicação como ZPL e EPL.
- http://www.youtube.com/watch?v=38hTwIm8Gvo - Identificação do enrolamento do ribbon para ser utilização na LB-1000.
- http://youtu.be/3PYLGsyN4XQ - Abastecimento de papel - Impressora de Etiquetas LB-1000.
- http://youtu.be/dUonC-x4Ixk - Abastecimento de ribbon - Impressora de Etiquetas LB-1000.

Para baixar a dll para a impressora LB-1000 acesse o site http://www.bematech.com.br/administrador/files/equipamento/suporte/15/1394146256-Impressora%20de%20etiquetas_LB-1000_Driver_03_Win_DLL.zip.

DLL's, drivers e manuais: http://www.bematech.com.br/suporte/equipamento/lb-1000

## Confira agora alguns exemplos de programação em Delphi e Visual Basic sobre a LB-1000.

Primeiramente deixe a dll sempre junto com o executável do sistema que está desenvolvendo, assim é mais confiável a questão de que o seu sistema sempre vai buscar diretamente da pasta que esta alocado o executável.

### Declaração em Delphi:

```
procedure openport(PrinterName:pchar);stdcall;far; external 'tsclib.dll';
procedure closeport; external 'tsclib.dll';
procedure sendcommand(Command:pchar);stdcall;far;external 'tsclib.dll';
procedure setup(LabelWidth, LabelHeight, Speed, Density, Sensor, Vertical, Offset:pchar);stdcall; far; external 'tsclib.dll';
procedure downloadpcx(Filename,ImageName:pchar);stdcall;far;external 'tsclib.dll';
procedure barcode(X, Y, CodeType, Height, Readable, Rotation, Narrow, Wide, Code :pchar); stdcall; far; external 'tsclib.dll';
procedure printerfont(X, Y, FontName, Rotation, Xmul, Ymul, Content:pchar);stdcall;far; external 'tsclib.dll';
procedure clearbuffer; external 'tsclib.dll';
procedure printlabel(NumberOfSet, NumberOfCopoy:pchar);stdcall; far;external 'tsclib.dll';
procedure formfeed;external 'tsclib.dll';
procedure nobackfeed; external 'tsclib.dll';
procedure windowsfont (X, Y, FontHeight, Rotation, FontStyle, FontUnderline : integer; FaceName, TextContect:pchar);stdcall;far;external 'tsclib.dll';
No botão colocar a seguinte rotina:
procedure TForm1.Button1Click(Sender: TObject);
var
i: Integer;
sPorta : string;
begin
sPorta := Edit1.Text;
openport(pchar(sPorta));
for i:=1 to 1 do
begin
setup('110', '21', '3.0', '12', '1', '1', '0');
sendcommand('SET TEAR ON');
sendcommand('DIRECTION 0');
clearbuffer;
windowsfont(15, 0, 30, 0, 2, 0, 'arial', 'xxxxxxxxxx');
barcode('25', '5', 'EAN13', '70', '1', '0', '2', '2', '111111111111');
windowsfont(315, 0, 30, 0, 2, 0, 'arial', 'Exemplo Bema2 ');
barcode('325', '5', 'EAN13', '70', '1', '0', '2', '2', '222222222222');
windowsfont(615, 0, 30, 0, 2, 0, 'arial', 'Exemplo Bema2 ');
barcode('620', '5', 'EAN13', '70', '1', '0', '2', '2', '333333333333');
printlabel('1', '1');
end;
closeport;
end;
```
 
### Declaração em Visual Basic:

```
Declare Sub openport Lib "C:\windows\system32\tsclib.dll" (ByVal PrinterName As String)
Declare Sub closeport Lib "C:\windows\system32\tsclib.dll" ()
Declare Sub sendcommand Lib "C:\windows\system32\tsclib.dll" (ByVal command As String)
Declare Sub setup Lib "C:\windows\system32\tsclib.dll" (ByVal LabelWidth As String, ByVal LabelHeight As String, ByVal Speed As String, ByVal Density As String, ByVal Sensor As String, ByVal Vertical As String, ByVal Offset As String)
Declare Sub downloadpcx Lib "C:\windows\system32\tsclib.dll" (ByVal Filename As String, ByVal ImageName As String)
Declare Sub barcode Lib "C:\windows\system32\tsclib.dll" (ByVal X As String, ByVal Y As String, ByVal CodeType As String, ByVal Height As String, ByVal Readable As String, ByVal rotation As String, ByVal Narrow As String, ByVal Wide As String, ByVal Code As String)
Declare Sub printerfont Lib "C:\windows\system32\tsclib.dll" (ByVal X As String, ByVal Y As String, ByVal FontName As String, ByVal rotation As String, ByVal Xmul As String, ByVal Ymul As String, ByVal Content As String)
Declare Sub clearbuffer Lib "C:\windows\system32\tsclib.dll" ()
Declare Sub printlabel Lib "C:\windows\system32\tsclib.dll" (ByVal NumberOfSet As String, ByVal NumberOfCopy As String)
Declare Sub formfeed Lib "C:\windows\system32\tsclib.dll" ()
Declare Sub nobackfeed Lib "C:\windows\system32\tsclib.dll" ()
Declare Sub windowsfont Lib "C:\windows\system32\tsclib.dll" (ByVal X As Integer, ByVal Y As Integer, ByVal fontheight As Integer, ByVal rotation As Integer, ByVal fontstyle As Integer, ByVal fontunderline As Integer, ByVal FaceName As String, ByVal TextContent As String)
No botão colocar a seguinte rotina:
Private Sub Command1_Click() 'PRINT LABEL
Dim PrintLabels As String
Dim sImagem As String
Call openport("USB")
Call setup("66", "30", "3.0", "12", "0", "0", "0")
Call clearbuffer
Call windowsfont(6, 10, 30, 0, 2, 0, "arial", "Exemplo em Visual Basic 6 - LB-1000 - Bematech")
Call barcode("10", "100", "128", "100", "1", "0", "2", "2", Text1.Text)
Call downloadpcx("Logo.pcx", "Logo.pcx")
Call sendcommand("PUTPCX 200, 80, ""Logo.pcx""")
Call printlabel("1", "1")
Call closeport
End Sub
```

Com essas rotinas já vai ser possível imprimir etiquetas, para configurar o tamanho dela, sugerimos que verifiquem o manual técnico de programação para as funções: setup, windowsfont, e barcode (para código de barras).

## ACBr 

Existem bibliotecas feitas pela ACBr, que facilitam ou não o desenvolvimento de produtos na direção de diversas impressoras do mercado.

### ACBrETQ
