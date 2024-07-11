## O código a seguir tem como o objetivo de ter um semáforo funcional, onde tenha os sinais verde, amarelo e vermelho.<br> Conta tambem com as funções de mudar o tipo do semáforo para com ou sem contagem digital em segundos (botão direito do mouse).
![imagem_2024-07-11_130852634](https://github.com/FernandoCMFilho/Semaforo/assets/54756245/11e486b2-8d99-441a-94e6-af7f39c86229) ![imagem_2024-07-11_131109291](https://github.com/FernandoCMFilho/Semaforo/assets/54756245/4b8c496d-1c1b-42c7-bcae-e397635488bb)
![imagem_2024-07-11_131242580](https://github.com/FernandoCMFilho/Semaforo/assets/54756245/61859eba-0e00-48f5-b019-9568d3ec93e3)

### Classe Janela
``` Java
package semaforo;

import java.awt.Color;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.MouseEvent;
import java.awt.event.MouseListener;
import javax.swing.JFrame;
import javax.swing.JMenu;
import javax.swing.JMenuItem;
import javax.swing.JPopupMenu;


public class Janela extends JFrame implements ActionListener,MouseListener{
    
    Desenho desenho;
    Carros carros;
    
    private JPopupMenu menu;
    
    private JMenu menuTipo;
    private JMenuItem Analogico;
    private JMenuItem Digital;
    
   private int Tipo;
    
    
    public Janela() {
        
        menu = new JPopupMenu();
        
        menuTipo = new JMenu("Tipo");
        
        Analogico = new JMenuItem("Analógico");
        Digital = new JMenuItem("DIgital");
        
        menuTipo.add(Analogico);
        menuTipo.add(Digital);
        
        menu.add(menuTipo);
        
        this.addMouseListener(this);
        
        Analogico.addActionListener(this);
        Digital.addActionListener(this);
        
        
        
        desenho = new Desenho(1, Color.red, Color.green);
        carros = new Carros();
        
       
        
        this.add(desenho);
        this.setSize(600,600);
        this.setLocationRelativeTo(null);
        this.setDefaultCloseOperation(EXIT_ON_CLOSE);
    }

    @Override
    public void mouseClicked(MouseEvent e) {
        if(e.getButton() == MouseEvent.BUTTON3){
            menu.show(this,e.getX(), e.getY());
        }
    }
    @Override
    public void mousePressed(MouseEvent e) {
       
    }

    @Override
    public void mouseReleased(MouseEvent e) {
        
    }

    @Override
    public void mouseEntered(MouseEvent e) {
        
    }

    @Override
    public void mouseExited(MouseEvent e) {
       
    }

    @Override
    public void actionPerformed(ActionEvent e) {
       if(e.getSource() == Analogico){
           Tipo = 0;
        }
        else if(e.getSource() == Digital){
            Tipo = 2;
        }
       desenho.setAn(Tipo);
    }
}
```
### Classe Desenho
``` Java

package semaforo;

import java.awt.Color;
import java.awt.Font;
import java.awt.Graphics;
import java.awt.Image;
import java.util.logging.Level;
import java.util.logging.Logger;
import javax.swing.ImageIcon;
import javax.swing.JComponent;

public class Desenho extends JComponent implements Runnable {

    private int forma;
    public Color cor;
    public Color cor2;
    private int px = 5, py = 5;
    private int direcao = 1;
    private int cont;
    public Object lock;
    public int estado;
    public int seg;
    public int segs = 20;
    private int Tipo;
    public Carros carros = new Carros();
    //Image flora, papoula;
    
    //String floram = "./src/<default package>/amare.png";
    
    public Desenho(int forma, Color cor, Color cor2) {
        this.forma = forma;
        this.cor = cor;
        this.cor2 = cor2;
        new Thread(this).start();
    }

    public Desenho(int Tipo) {
        this.Tipo = Tipo;
    }

    public int getAn() {
        return Tipo;
    }

    public void setAn(int Tipo) {
        this.Tipo = Tipo;
    }

    public Color getCor2() {
        return cor2;
    }

    public void setCor2(Color cor2) {
        this.cor2 = cor2;
    }

    public Color getCor() {
        return this.cor;
    }

    public void setCont(int cont) {
        this.cont = cont;
    }

    public void setForma(int forma) {
        this.forma = forma;
    }

    public void setCor(Color cor) {
        this.cor = cor;
    }
    

    public void paint(Graphics g) {

//Ruas

        g.fillRect(260, 0, 75, 600);
        g.fillRect(0, 240, 600, 75);
        g.setColor(Color.yellow); //Faixas amarelas
        g.fillRect(293, 0, 10, 40);
        g.fillRect(293, 60, 10, 40);
        g.fillRect(293, 120, 10, 40);
        g.fillRect(293, 180, 10, 40);
        g.fillRect(293, 240, 10, 40);
        g.fillRect(293, 300, 10, 40);
        g.fillRect(293, 360, 10, 40);
        g.fillRect(293, 420, 10, 40);
        g.fillRect(293, 480, 10, 40);
        g.fillRect(293, 540, 10, 40);
        g.fillRect(293, 600, 10, 40);
        g.fillRect(0, 272, 40, 10);
        g.fillRect(60, 272, 40, 10);
        g.fillRect(120, 272, 40, 10);
        g.fillRect(180, 272, 40, 10);
        g.fillRect(240, 272, 40, 10);
        g.fillRect(294, 272, 46, 10);
        g.fillRect(360, 272, 40, 10);
        g.fillRect(420, 272, 40, 10);
        g.fillRect(480, 272, 40, 10);
        g.fillRect(540, 272, 40, 10);
        g.fillRect(600, 272, 40, 10);
        g.setColor(Color.green); //Grama
        g.fillRect(0, 0, 260, 240);
        g.fillRect(335, 0, 260, 240);
        g.fillRect(0, 315, 260, 250);
        g.fillRect(335, 315, 260, 250);
        carros.paint(g);
        g.setColor(Color.BLACK);
        g.fillRect(98, 85, 5, 30);
        g.setColor(Color.red);
        g.fillRect(90, 75, 20, 20);
        g.setColor(Color.yellow);
        g.fillRect(97, 81, 6, 6);
        g.setColor(Color.black); //Fundo semafaro
        g.fillRect(380, 235, 40, 85);
        g.fillRect(255, 160, 85, 40);
        if (this.Tipo == 2) {
            g.fillRect(255, 140, 85, 40);
            g.fillRect(400, 235, 40, 85);
        }

        g.setColor(Color.gray); //hastes
        g.fillRect(340, 175, 45, 10);
        g.fillRect(210, 175, 45, 10);
        g.fillRect(375, 175, 10, 25);
        g.fillRect(210, 175, 10, 30);
        g.fillRect(395, 190, 10, 45);
        g.fillRect(395, 320, 10, 45);
        g.fillRect(365, 355, 30, 10);
        g.fillRect(385, 190, 20, 10);
        g.setColor(Color.GRAY);
        g.fillOval(390, 290, 20, 20); //vermelho
        g.fillOval(390, 265, 20, 20); //Amarelo
        g.fillOval(390, 240, 20, 20); //Verde
        g.fillOval(260, 170, 20, 20); //vermelho
        g.fillOval(285, 170, 20, 20); //Amarelo
        g.fillOval(310, 170, 20, 20); //Verde
        g.setFont(new Font("Helvetica", Font.BOLD, 18));
        //g.drawImage(flora, 150, 150, this);

        if (cor == Color.green) {
            g.setColor(cor);
            g.fillOval(390, 290, 20, 20);
            if (this.Tipo == 2) {
                g.drawString(Segs(), 415, 307);
            }
        } else if (cor == Color.red) {
            g.setColor(cor);
            g.fillOval(390, 240, 20, 20);
            if (this.Tipo==2){
            g.drawString(Segs(), 414, 256);}
        } else if (cor == Color.yellow) {
            g.setColor(Color.yellow);
            g.fillOval(390, 265, 20, 20);
            if (this.Tipo==2){
            g.drawString(Segs(), 414, 283);}
        }
        if (cor2 == Color.green) {
            g.setColor(cor2);
            g.fillOval(260, 170, 20, 20);
            if (this.Tipo==2){
            g.drawString(Segs(), 259, 163);}
        } else if (cor2 == Color.yellow) {
            g.setColor(cor2);
            g.fillOval(285, 170, 20, 20);
            if (this.Tipo==2){
            g.drawString(Segs(), 285, 163);}
        } else if (cor2 == Color.red) {
            g.setColor(cor2);
            g.fillOval(310, 170, 20, 20);
            if (this.Tipo==2){
            g.drawString(Segs(), 310, 163);}
        }

    }

    @Override

    public void run() {

        while (true) {
            try {
                if (cont == 20) {
                    if (cor == Color.red) {
                        cor = Color.green;
                    } else if (cor == Color.yellow) {
                        cor = Color.red;
                    }
                    if (cor2 == Color.red) {
                        cor2 = Color.green;
                    } else if (cor2 == Color.yellow) {
                        cor2 = Color.red;

                    }

                    cont = 0;
                    estado = 0;
                    segs = 20;
                    repaint();
                }
                if (estado == 14) {
                    if (cor == Color.green) {
                        cor = Color.yellow;
                    }
                    if (cor2 == Color.green) {
                        cor2 = Color.yellow;
                    }
                    repaint();

                }
                cont++;
                estado++;
                segs--;
                repaint();

                Thread.sleep(1000);
            } catch (InterruptedException ex) {
                System.out.println("oi");
            }

        }
    }
    

    public String Segs() {
        if (segs <= 9) {
            return "0" + segs;
        } else if (segs >= 10) {
            return Integer.toString(segs);
        }
        return null;
    }

}
```
### Classe Semaforo
``` Java

package semaforo;

public class Semaforo {

    public static void main(String[] args) {
        new Janela().setVisible(true);
    }
    
}
```




