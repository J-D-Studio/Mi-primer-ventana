# Mi-primer-ventana

    package Java.UIsmd;

    import javax.swing.*;      
    import java.awt.*;

    public class SistemaCompleto extends JFrame {
    
    private final CardLayout cardLayout;
    private final JPanel cardsPanel;
    
    public SistemaCompleto() {
        setTitle("Sistema Completo de GestiÃ³n");
        setSize(800, 600);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        
        // Configurar layout principal
        setLayout(new BorderLayout());
        
        // 1. BARRA DE MENÃš SUPERIOR
        JMenuBar menuBar = crearMenuBar();
        setJMenuBar(menuBar);
        
        // 2. PANEL DE NAVEGACIÃ“N IZQUIERDO
        JPanel panelNavegacion = crearPanelNavegacion();
        add(panelNavegacion, BorderLayout.WEST);
        
        // 3. PANEL DE CONTENIDO CENTRAL (con CardLayout)
        cardLayout = new CardLayout();
        cardsPanel = new JPanel(cardLayout);
        
        // Crear todas las pantallas
        cardsPanel.add(crearPantallaInicio(), "INICIO");
        cardsPanel.add(crearPantallaUsuarios(), "USUARIOS");
        cardsPanel.add(crearPantallaProductos(), "PRODUCTOS");
        cardsPanel.add(crearPantallaVentas(), "VENTAS");
        cardsPanel.add(crearPantallaConfiguracion(), "CONFIG");
        cardsPanel.add(crearPantallaAyuda(), "AYUDA");
        
        add(cardsPanel, BorderLayout.CENTER);
        
        // 4. BARRA DE ESTADO INFERIOR
        add(crearBarraEstado(), BorderLayout.SOUTH);
        
        setVisible(true);
    }
    
    private JMenuBar crearMenuBar() {
        JMenuBar menuBar = new JMenuBar();
        
        // MenÃº Archivo
        JMenu menuArchivo = new JMenu("Archivo");
        menuArchivo.add(new JMenuItem("Nuevo"));
        menuArchivo.add(new JMenuItem("Abrir"));
        menuArchivo.addSeparator();
        menuArchivo.add(new JMenuItem("Salir"));
        
        // MenÃº Editar
        JMenu menuEditar = new JMenu("Editar");
        menuEditar.add(new JMenuItem("Copiar"));
        menuEditar.add(new JMenuItem("Pegar"));
        menuEditar.add(new JMenuItem("Eliminar"));
        
        // MenÃº Ver
        JMenu menuVer = new JMenu("Ver");
        JCheckBoxMenuItem itemToolbar = new JCheckBoxMenuItem("Barra de herramientas", true);
        JCheckBoxMenuItem itemStatus = new JCheckBoxMenuItem("Barra de estado", true);
        menuVer.add(itemToolbar);
        menuVer.add(itemStatus);
        
        // MenÃº Ayuda
        JMenu menuAyuda = new JMenu("Ayuda");
        menuAyuda.add(new JMenuItem("DocumentaciÃ³n"));
        menuAyuda.add(new JMenuItem("Acerca de..."));
        
        menuBar.add(menuArchivo);
        menuBar.add(menuEditar);
        menuBar.add(menuVer);
        menuBar.add(menuAyuda);
        
        return menuBar;
    }
    
    private JPanel crearPanelNavegacion() {
        JPanel panel = new JPanel();
        panel.setLayout(new GridLayout(10, 1, 5, 5));
        panel.setBorder(BorderFactory.createTitledBorder("NavegaciÃ³n"));
        panel.setPreferredSize(new Dimension(150, 0));
        panel.setBackground(new Color(240, 240, 240));
        
        String[] opciones = {
            "ðŸ  Inicio",
            "ðŸ‘¥ Usuarios", 
            "ðŸ“¦ Productos",
            "ðŸ’° Ventas",
            "ðŸ“Š Reportes",
            "âš™ï¸ ConfiguraciÃ³n",
            "â“ Ayuda",
            "ðŸ“‹ Acerca de",
            "ðŸ”„ Actualizar",
            "ðŸšª Salir"
        };
        
        for (String opcion : opciones) {
            JButton btn = new JButton(opcion);
            btn.setHorizontalAlignment(SwingConstants.LEFT);
            btn.addActionListener(e -> {
                String texto = btn.getText();
                cambiarPantalla(texto);
            });
            panel.add(btn);
        }
        
        return panel;
    }
    
    private void cambiarPantalla(String opcion) {
        switch(opcion) {
            case "ðŸ  Inicio": cardLayout.show(cardsPanel, "INICIO"); break;
            case "ðŸ‘¥ Usuarios": cardLayout.show(cardsPanel, "USUARIOS"); break;
            case "ðŸ“¦ Productos": cardLayout.show(cardsPanel, "PRODUCTOS"); break;
            case "ðŸ’° Ventas": cardLayout.show(cardsPanel, "VENTAS"); break;
            case "âš™ï¸ ConfiguraciÃ³n": cardLayout.show(cardsPanel, "CONFIG"); break;
            case "â“ Ayuda": cardLayout.show(cardsPanel, "AYUDA"); break;
        }
    }
    
    // ========== PANTALLAS INDIVIDUALES ==========
    
    private JPanel crearPantallaInicio() {
        JPanel panel = new JPanel(new BorderLayout());
        
        // Encabezado
        JLabel titulo = new JLabel("BIENVENIDO AL SISTEMA", SwingConstants.CENTER);
        titulo.setFont(new Font("Arial", Font.BOLD, 24));
        titulo.setForeground(new Color(0, 100, 200));
        
        // Panel de estadÃ­sticas
        JPanel statsPanel = new JPanel(new GridLayout(2, 3, 10, 10));
        String[] stats = {"Usuarios: 156", "Productos: 892", "Ventas Hoy: $5,430", 
                         "Pedidos Pendientes: 12", "Stock Bajo: 8", "Clientes Nuevos: 3"};
        
        for (String stat : stats) {
            JPanel card = new JPanel(new BorderLayout());
            card.setBorder(BorderFactory.createLineBorder(Color.GRAY));
            card.setBackground(Color.WHITE);
            
            JLabel label = new JLabel(stat, SwingConstants.CENTER);
            label.setFont(new Font("Arial", Font.PLAIN, 14));
            card.add(label, BorderLayout.CENTER);
            
            statsPanel.add(card);
        }
        
        // Panel de accesos rÃ¡pidos
        JPanel quickPanel = new JPanel(new FlowLayout());
        String[] quickActions = {"Nueva Venta", "Agregar Producto", "Ver Reportes", "Clientes"};
        
        for (String action : quickActions) {
            JButton btn = new JButton(action);
            btn.setPreferredSize(new Dimension(120, 40));
            quickPanel.add(btn);
        }
        
        panel.add(titulo, BorderLayout.NORTH);
        panel.add(statsPanel, BorderLayout.CENTER);
        panel.add(quickPanel, BorderLayout.SOUTH);
        
        return panel;
    }
    
    private JPanel crearPantallaUsuarios() {
        JPanel panel = new JPanel(new BorderLayout());
        
        // Toolbar
        JPanel toolbar = new JPanel(new FlowLayout(FlowLayout.LEFT));
        toolbar.add(new JButton("âž• Agregar"));
        toolbar.add(new JButton("âœï¸ Editar"));
        toolbar.add(new JButton("ðŸ—‘ï¸ Eliminar"));
        toolbar.add(new JButton("ðŸ”„ Actualizar"));
        
        // Tabla de usuarios
        String[] columnas = {"ID", "Nombre", "Email", "Rol", "Fecha Registro"};
        Object[][] datos = {
            {"001", "Juan PÃ©rez", "juan@email.com", "Administrador", "2024-01-15"},
            {"002", "MarÃ­a GarcÃ­a", "maria@email.com", "Vendedor", "2024-02-20"},
            {"003", "Carlos LÃ³pez", "carlos@email.com", "Cliente", "2024-03-10"}
        };
        
        JTable tabla = new JTable(datos, columnas);
        JScrollPane scrollPane = new JScrollPane(tabla);
        
        panel.add(new JLabel("ðŸ‘¥ GESTIÃ“N DE USUARIOS", SwingConstants.CENTER), BorderLayout.NORTH);
        panel.add(toolbar, BorderLayout.NORTH);
        panel.add(scrollPane, BorderLayout.CENTER);
        
        return panel;
    }
    
    private JPanel crearPantallaProductos() {
        JPanel panel = new JPanel(new BorderLayout());
        
        // Formulario de producto
        JPanel formPanel = new JPanel(new GridLayout(4, 2, 10, 10));
        formPanel.setBorder(BorderFactory.createTitledBorder("Nuevo Producto"));
        
        formPanel.add(new JLabel("Nombre:"));
        formPanel.add(new JTextField(20));
        formPanel.add(new JLabel("Precio:"));
        formPanel.add(new JTextField(10));
        formPanel.add(new JLabel("CategorÃ­a:"));
        String[] categorias = {"ElectrÃ³nica", "Ropa", "Alimentos", "Hogar"};
        formPanel.add(new JComboBox<>(categorias));
        formPanel.add(new JLabel("Stock:"));
        formPanel.add(new JTextField(10));
        
        // Botones del formulario
        JPanel btnPanel = new JPanel();
        btnPanel.add(new JButton("Guardar"));
        btnPanel.add(new JButton("Cancelar"));
        
        panel.add(new JLabel("ðŸ“¦ GESTIÃ“N DE PRODUCTOS", SwingConstants.CENTER), BorderLayout.NORTH);
        panel.add(formPanel, BorderLayout.WEST);
        panel.add(btnPanel, BorderLayout.SOUTH);
        
        return panel;
    }
    
    private JPanel crearPantallaVentas() {
        JPanel panel = new JPanel(new BorderLayout());
        
        // Panel izquierdo: Carrito de compras
        JPanel carritoPanel = new JPanel(new BorderLayout());
        carritoPanel.setBorder(BorderFactory.createTitledBorder("Carrito de Compras"));
        
        DefaultListModel<String> carritoModel = new DefaultListModel<>();
        carritoModel.addElement("Producto A - $100 x2 = $200");
        carritoModel.addElement("Producto B - $50 x1 = $50");
        carritoModel.addElement("Producto C - $75 x3 = $225");
        
        JList<String> carritoList = new JList<>(carritoModel);
        carritoPanel.add(new JScrollPane(carritoList), BorderLayout.CENTER);
        
        JPanel totalPanel = new JPanel(new FlowLayout(FlowLayout.RIGHT));
        totalPanel.add(new JLabel("Total: $475"));
        totalPanel.add(new JButton("Finalizar Venta"));
        carritoPanel.add(totalPanel, BorderLayout.SOUTH);
        
        // Panel derecho: BÃºsqueda de productos
        JPanel busquedaPanel = new JPanel(new BorderLayout());
        busquedaPanel.setBorder(BorderFactory.createTitledBorder("Buscar Productos"));
        
        JPanel searchBar = new JPanel(new BorderLayout());
        searchBar.add(new JTextField("Buscar producto..."), BorderLayout.CENTER);
        searchBar.add(new JButton("ðŸ”"), BorderLayout.EAST);
        
        busquedaPanel.add(searchBar, BorderLayout.NORTH);
        
        panel.add(new JLabel("ðŸ’° PUNTO DE VENTA", SwingConstants.CENTER), BorderLayout.NORTH);
        panel.add(carritoPanel, BorderLayout.WEST);
        panel.add(busquedaPanel, BorderLayout.CENTER);
        
        return panel;
    }
    
    private JPanel crearPantallaConfiguracion() {
        JPanel panel = new JPanel(new GridLayout(3, 2, 20, 20));
        panel.setBorder(BorderFactory.createEmptyBorder(20, 20, 20, 20));
        
        // Opciones de configuraciÃ³n
        String[] configs = {
            "Tema de la aplicaciÃ³n:",
            "Idioma:",
            "Moneda:",
            "Formato de fecha:",
            "Backup automÃ¡tico:",
            "Notificaciones:"
        };
        
        for (String config : configs) {
            JPanel itemPanel = new JPanel(new BorderLayout());
            itemPanel.add(new JLabel(config), BorderLayout.WEST);
            
            if (config.contains("Tema")) {
                JComboBox<String> temas = new JComboBox<>(new String[]{"Claro", "Oscuro", "Azul"});
                itemPanel.add(temas, BorderLayout.EAST);
            } else if (config.contains("Backup") || config.contains("Notificaciones")) {
                JCheckBox check = new JCheckBox();
                check.setSelected(true);
                itemPanel.add(check, BorderLayout.EAST);
            } else {
                itemPanel.add(new JTextField(15), BorderLayout.EAST);
            }
            
            panel.add(itemPanel);
        }
        
        JPanel mainPanel = new JPanel(new BorderLayout());
        mainPanel.add(new JLabel("âš™ï¸ CONFIGURACIÃ“N DEL SISTEMA", SwingConstants.CENTER), BorderLayout.NORTH);
        mainPanel.add(panel, BorderLayout.CENTER);
        
        JPanel btnPanel = new JPanel();
        btnPanel.add(new JButton("Guardar Cambios"));
        btnPanel.add(new JButton("Restaurar Predeterminados"));
        mainPanel.add(btnPanel, BorderLayout.SOUTH);
        
        return mainPanel;
    }
    
    private JPanel crearPantallaAyuda() {
        JPanel panel = new JPanel(new BorderLayout());
        
        JTextArea areaAyuda = new JTextArea();
        areaAyuda.setText("MANUAL DE USUARIO\n\n" +
                         "1. GestiÃ³n de Usuarios:\n" +
                         "   - Agregar nuevos usuarios\n" +
                         "   - Editar informaciÃ³n existente\n" +
                         "   - Asignar roles y permisos\n\n" +
                         "2. GestiÃ³n de Productos:\n" +
                         "   - Registrar nuevos productos\n" +
                         "   - Actualizar inventario\n" +
                         "   - Gestionar categorÃ­as\n\n" +
                         "3. Ventas:\n" +
                         "   - Procesar ventas rÃ¡pidas\n" +
                         "   - Generar facturas\n" +
                         "   - Ver historial\n\n" +
                         "Para mÃ¡s ayuda, contacte al administrador.");
        
        areaAyuda.setEditable(false);
        
        panel.add(new JLabel("â“ CENTRO DE AYUDA", SwingConstants.CENTER), BorderLayout.NORTH);
        panel.add(new JScrollPane(areaAyuda), BorderLayout.CENTER);
        
        JPanel contactoPanel = new JPanel(new FlowLayout());
        contactoPanel.add(new JLabel("Soporte tÃ©cnico: soporte@empresa.com | Tel: 555-1234"));
        panel.add(contactoPanel, BorderLayout.SOUTH);
        
        return panel;
    }
    
    private JPanel crearBarraEstado() {
        JPanel panel = new JPanel(new BorderLayout());
        panel.setBorder(BorderFactory.createEtchedBorder());
        
        JLabel estado = new JLabel(" Estado: Conectado | Usuario: Admin | ");
        JLabel hora = new JLabel(new java.util.Date().toString());
        
        panel.add(estado, BorderLayout.WEST);
        panel.add(hora, BorderLayout.EAST);
        
        return panel;
    }
    
    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            @SuppressWarnings("unused")
            SistemaCompleto frame = new SistemaCompleto();
        });
    }
}
