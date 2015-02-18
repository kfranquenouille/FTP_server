package server;

import java.io.IOException;
import java.net.ServerSocket;
import java.net.Socket;

import exception.ServerAlreadyStartedException;

/**
 * @author franquenouille
 *
 */
public class Server {
	
	private boolean status = false;
	private ServerSocket ss;
	private Socket socket;
	
    /**
     * 
     * @param port
     * @throws IOException
     */
	public Server(int port) throws ServerAlreadyStartedException {
		try {
			this.ss = new ServerSocket(port);			
		} catch(IOException e) {
			throw new ServerAlreadyStartedException();
		}
	}
	
	/**
	 * getter de la socket du serveur
	 * @return
	 */
	public ServerSocket getServer() {
		return ss;
	}
	
	/**
	 * Affiche l'etat du serveur
	 * @return
	 */
	public boolean isStarted(){
		return this.status;
	}

	/**
	 * Permet de demarrer le serveur FTP
	 */
	public void startServer() throws ServerAlreadyStartedException {
		boolean isClosedServerSocket = false;
		if(!this.isStarted()) {
			this.status = true;
			System.out.println("The server is started on 127.0.0.1:3377");
			while (!isClosedServerSocket) {
				try {
					this.socket = this.getServer().accept();
					System.out.println("A client is connected to the Port "+this.socket.getPort());
					new Thread(new FtpClient(socket)).start();
				} catch (IOException e) {
					System.out.println("le server est fermé !");
					isClosedServerSocket = true;
				}
			}	
		} else {
			throw new ServerAlreadyStartedException();
		}
	}

	public void stop() {
		try {
			this.ss.close();
			this.status = false;
		} catch (IOException e) {
			e.printStackTrace();
		}
	}

	public static void main(String[] args) {
		try {
			Server serv = new Server(3377);
			serv.startServer();
		} catch (ServerAlreadyStartedException e) {
			System.out.println("Error : The server is already started");
		} 	
	}

}
