Servlet-Oracle
==============

Un código en Java con Servlet conectado a un majeador de base de datos en este caso Oracle

import java.io.IOException;
import java.io.PrintWriter;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.sql.*;


@WebServlet(name = "Datos", urlPatterns = {"/Datos"})
public class Datos extends HttpServlet {
        Connection conexion;
	Statement st;
	ResultSet rs;
	String ruta ="jdbc:oracle:thin:@localhost:1521:XE";
	String usuario = "CONSTANTE";
	String id1,ed,pass="ska";

    protected void processRequest(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("text/html;charset=UTF-8");
        PrintWriter out = response.getWriter();
        try {
	     String usuari = request.getParameter("user");
        Class.forName("oracle.jdbc.driver.OracleDriver");
	conexion = DriverManager.getConnection (ruta, usuario, pass);
        st = (Statement) conexion.createStatement(ResultSet.TYPE_SCROLL_INSENSITIVE, ResultSet.CONCUR_UPDATABLE);
        String min = "select * from \"Datos1\"  WHERE USUARIO = '"+usuari+"'";
        rs = st.executeQuery(min);
        
            while (rs.next()) {
           
            String nomb = rs.getString(1);
            String  usr= rs.getString(2);
            //String pass = rs.getString(3);
            String  ent= rs.getString(4);
            String  cor= rs.getString(5);
               
             String con = request.getParameter("pass");
             if(usuari.compareTo(usr)==0 && con.compareTo(pass)==0)
              {
                  if(ent.compareTo("MAESTRO")==0)
                          {
            out.println("<html>");
            out.println("<head>");
            out.println(" <title>Plataforma UVQ</title>");  
            out.println("<link rel='stylesheet' type='text/css' href='plat.css' />");
            out.println("<meta http-equiv='Content-Type' content='text/html' charset='UTF-8'>");  
            out.println("<LINK REL='SHORTCUT ICON' HREF='favicon.ico'>");
            out.println("</head>");
            out.println("<body>");
            out.println("<h1>Hola  "+ent+"  "+nomb+"</h1>");
            out.println("<h1>Clases Pendientes</h1>");
            String m= "select * from \"CLASES\"  WHERE "+ent+" = '"+nomb+"'";
               
            rs = st.executeQuery(m);
             while (rs.next()) {
            String tem = rs.getString(1);
            String  obj= rs.getString(2);
            String hi = rs.getString(3);
            String  hf= rs.getString(4);
            String  ta= rs.getString(5);
            String  fe= rs.getString(6);
            String ma = rs.getString(7);
            String  es= rs.getString(8);
              out.println("<h1>Tema: " +tem + "</h1>");
              out.println("<h1>Objetivo: " +obj + "</h1>");
              out.println("<h1>Hora Inicio: " +hi + "</h1>");
              out.println("<h1>Hora Final: " +hf + "</h1>");
              out.println("<h1>Tarea: " +ta+ "</h1>");
              out.println("<h1>Fecha: " +fe + "</h1>");
              out.println("<h1>Maestro: " +ma + "</h1>");
              out.println("<h1>Estudiante:" +es + "</h1>");
              out.println("</body>");
              out.println("</html>");
					
             }
            out.println("<html>");
            out.println("<head>");
            out.println("<title>Plataforma UVQ</title>");  
            out.println("<link rel='stylesheet' type='text/css' href='plat.css' />");
            out.println("<meta http-equiv='Content-Type' content='text/html' charset='UTF-8'>");  
            out.println("<LINK REL='SHORTCUT ICON' HREF='favicon.ico'>");
            out.println("</head>");
            out.println("<h1>Registrar Clase</h1>");
            out.println("<form  method='post'  action='Clase' name='form'>");
            out.println("<table id='ta' >");
            out.println("<tr>");
            out.println("<td>Tema :</td>");	
            out.println(" <td><input name='tema' type='text' size='20' required /></td>");					
            out.println("</tr>");
            out.println("<tr>");
            out.println("<td>Objetivo:</td>");
            out.println(" <td><input name='obj' type='text' size='20' required /></td>");
            out.println("</tr>");
            out.println("<tr>");
            out.println("<td>Hora de Inicio :</td>");
            out.println(" <td><input name='horaini' id='form_time' type='time' />  </td>");
            out.println("</tr>");
            out.println("<tr>");
            out.println("<td>Hora Final :</td>");
            out.println(" <td><input name='horafin' id='form_time' type='time' required />  </td>");
            out.println("</tr>");
            out.println("<tr>");
            out.println("<td>Tarea :</td>");
            out.println(" <td><input name='tarea' type='text' size='20' required /></td>");
            out.println("</tr>");
            out.println("<tr>");
            out.println("<td>Fecha:</td>");
            out.println(" <td><input name='fecha'  id='form_date' type='date' required /></td>");
            out.println("</tr>");
            out.println("<tr>");
            out.println("<td>Mestro :</td>");
            out.println(" <td><input name='mae' type='text' size='20' required /></td>");
            out.println("</tr>");
            out.println("<tr>");
            out.println("<td>Estudiante :</td>");
            out.println(" <td><input name='est' type='text' size='20' required /></td>");
            out.println("</tr>");
            out.println("</table>");
            out.println("<input type='submit' value='Registrar Clase' id='submit'/>");
            out.println("</form>");
            out.println("</body>");
            out.println("</html>");     
                          }
                  else{
            out.println("<html>");
            out.println("<head>");
            out.println(" <title>Plataforma UVQ</title>");  
            out.println("<link rel='stylesheet' type='text/css' href='plat.css' />");
            out.println("<meta http-equiv='Content-Type' content='text/html' charset='UTF-8'>");  
            out.println("<LINK REL='SHORTCUT ICON' HREF='favicon.ico'>");
            out.println("</head>");
            out.println("<body>");
            out.println("<h1>Hola  "+ent+"  "+nomb+"</h1>");
            out.println("<h1>Clases Pendientes</h1>");
            String m= "select * from \"CLASES\"  WHERE "+ent+" = '"+nomb+"'";
               
            rs = st.executeQuery(m);
            while (rs.next()) {
            String tem = rs.getString(1);
            String  obj= rs.getString(2);
            String hi = rs.getString(3);
            String  hf= rs.getString(4);
            String  ta= rs.getString(5);
             String  fe= rs.getString(6);
            String ma = rs.getString(7);
            String  es= rs.getString(8);
            
              out.println("<h1>Tema: " +tem + "</h1>");
              out.println("<h1>Objetivo: " +obj + "</h1>");
              out.println("<h1>Hora Inicio: " +hi + "</h1>");
              out.println("<h1>Hora Final: " +hf + "</h1>");
              out.println("<h1>Tarea: " +ta+ "</h1>");
              out.println("<h1>Fecha: " +fe + "</h1>");
              out.println("<h1>Maestro: " +ma + "</h1>");
              out.println("<h1>Estudiante:" +es + "</h1>");
           out.println("</body>");
            out.println("</html>");
					   
             }
                  
              }
              }
             else{
            out.println("<html>");
            out.println("<title>login</title>");  
            out.println("<body>");    
            out.println("<h1>No estas registrado, Registrate!!/h1>");
            out.println("<form  method='post'  action='Alta' name='form'>");
            out.println("<table id='ta' >");
            out.println("<tr>");
            out.println("<td>Entidad :</td>");
            out.println("<input type='radio'  value='MAESTRO' name='ocupacion'>Maestro<br>");			
            out.println("<input type='radio'  value='ESTUDIANTE' name='ocupacion'>Estudiante<br>");				
            out.println("</td>");					
            out.println("</tr>");
            out.println("<tr>");
            out.println("<td>Nombre :</td>");
            out.println(" <td><input name='nom' type='text' size='20' required /></td>");
            out.println("</tr>");
            out.println("<tr>");
            out.println("<td>Usuario :</td>");
            out.println(" <td><input name='user' type='text' size='20' required /></td>");
            out.println("</tr>");
            out.println("<tr>");
            out.println("<td>Contraseña :</td>");
            out.println("   <td><input name='pass' type='password' size='20' required/></td>");
            out.println("</tr>");
            out.println("<tr>");
            out.println("<td>Correo :</td>");
            out.println(" <td><input name='correo' type='text' size='20' required /></td>");
            out.println("</tr>");
            out.println("</table>");
            out.println("<input type='submit' value='Registrarse' id='submit'/>");
            out.println("</form>");
            out.println("</body>");
            out.println("</html>");
							
						
             }
                     
           }    
	} 
	catch (ClassNotFoundException e1) {
                
		out.println("ERROR:No encuentro el driver de la BD: "+
				e1.getMessage());
	}
	catch (SQLException e2) {
                //Error SQL: login/passwd mal
		out.println("ERROR:Fallo en SQL: "+e2.getMessage());
	}
	finally {
            
		try {
			if (conexion!=null)
				conexion.close();
		} catch (SQLException e3) {
			out.println("ERROR:Fallo al desconectar de la BD: "+
				e3.getMessage());
		}
	
	}
    
    }

    // <editor-fold defaultstate="collapsed" desc="HttpServlet methods. Click on the + sign on the left to edit the code.">
    /**
     * Handles the HTTP
     * <code>GET</code> method.
     *
     * @param request servlet request
     * @param response servlet response
     * @throws ServletException if a servlet-specific error occurs
     * @throws IOException if an I/O error occurs
     */
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        processRequest(request, response);
    }

    /**
     * Handles the HTTP
     * <code>POST</code> method.
     *
     * @param request servlet request
     * @param response servlet response
     * @throws ServletException if a servlet-specific error occurs
     * @throws IOException if an I/O error occurs
     */
    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        processRequest(request, response);
    }

    /**
     * Returns a short description of the servlet.
     *
     * @return a String containing servlet description
     */
    @Override
    public String getServletInfo() {
        return "Short description";
    }// </editor-fold>
}

		

 
