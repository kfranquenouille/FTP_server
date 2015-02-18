package test.tools;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;
import java.io.PrintWriter;
import java.net.InetAddress;
import java.net.Socket;
/**
 * 
 * Simulation d'un client FTP afin de pour lancer les tests sur les requetes.
 *
 */
public class ClientUtil {

	private InetAddress address;
	public Socket socket;
	private BufferedReader reader;
	private PrintWriter writer;
	private String root;
	
	/**
	 * 
	 * @param port
	 */
	public ClientUtil(final int port) {
		try {
			this.root="/";
			this.address = InetAddress.getLocalHost();
			this.socket = new Socket(this.address, port);
			this.writer = new PrintWriter(new OutputStreamWriter(this.socket.getOutputStream()), true);
			this.reader = new BufferedReader(new InputStreamReader(this.socket.getInputStream()));
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
	
	/**
	 * Permet de simuler l'envoi d'une requete ftp sur un serveur
	 * @param ftp request
	 */
	public void sendRequest(final String request) {
		this.writer.println(request);
	}
	
	/**
	 * Permet de simuler la reception d'une requete sur le client FTP
	 * @return message returned from the server
	 */
	public String receiveRequest() {
		String returnMessage=null;
		try {
			returnMessage = this.reader.readLine();
		} catch (IOException e) {
			e.printStackTrace();
		}
		return returnMessage;
	}
	
	/**
	 * Ferme toute la simulation d'un client FTP
	 */
	public void closeAll(){
		try {
			this.reader.close();
			this.writer.close();
			this.socket.close();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
	
	/**
	 * private test
	 * don't be afraid about this :)
	 */
	public static void main(String[] args) {
			
		// Client
		System.out.println("On peut tester le client !");
		ClientUtil cli = new ClientUtil(3377);
//		System.out.println("getLocalPort()....: "+cli.socket.getLocalPort());
//		System.out.println("PORT 127,0,0,1,"+(cli.socket.getLocalPort() >> 8)+","+(cli.socket.getLocalPort() & 255));
		try {
			Thread.sleep(5000);
		} catch (InterruptedException e) {
			System.out.println("Le server a rencontré un problème de thread");
			System.exit(0);
		}	
		System.out.println("MSG reçu : "+cli.receiveRequest());
		
		// Connexion
		cli.sendRequest("USER test");
		System.out.println("MSG reçu : "+cli.receiveRequest());
		cli.sendRequest("PASS test");
		System.out.println("MSG reçu : "+cli.receiveRequest());

		// ls
		int localport = cli.socket.getLocalPort()+1;
		cli.sendRequest("PORT 127,0,0,1,"+(localport >> 8)+","+(localport & 255));
		System.out.println("MSG reçu : "+cli.receiveRequest());		
		cli.sendRequest("NLST");
		System.out.println("MSG reçu : "+cli.receiveRequest());
		
		cli.closeAll();
	}
}
