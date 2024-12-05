# Tugas 14 PBO
Nama  : Muhammad Irsyad Habibi

NRP  : 5025221150

Kelas  : PBO A

# Membuat frame windows user login dan password

Program berikut mengimplementasikan pembuatan aplikasi dengan jendela login yang memiliki dua field: Username dan Password, serta tombol Login.
```
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class LoginFrame extends JFrame {
    public LoginFrame() {
        // Mengatur judul frame
        setTitle("User Login");
        setSize(300, 200);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        // Panel utama
        JPanel panel = new JPanel();
        panel.setLayout(new GridLayout(3, 2, 10, 10));

        // Label dan field untuk username
        JLabel userLabel = new JLabel("Username:");
        JTextField userField = new JTextField();
        panel.add(userLabel);
        panel.add(userField);

        // Label dan field untuk password
        JLabel passLabel = new JLabel("Password:");
        JPasswordField passField = new JPasswordField();
        panel.add(passLabel);
        panel.add(passField);

        // Tombol login
        JButton loginButton = new JButton("Login");
        panel.add(new JLabel()); // Placeholder
        panel.add(loginButton);

        // Tambahkan panel ke frame
        add(panel);

        // Tambahkan listener untuk tombol login
        loginButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String username = userField.getText();
                String password = new String(passField.getPassword());

                // Contoh validasi sederhana
                if (username.equals("admin") && password.equals("1234")) {
                    JOptionPane.showMessageDialog(null, "Login successful!");
                } else {
                    JOptionPane.showMessageDialog(null, "Invalid username or password.", "Error", JOptionPane.ERROR_MESSAGE);
                }
            }
        });
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            LoginFrame frame = new LoginFrame();
            frame.setVisible(true);
        });
    }
}
```

Komponen:
- `JLabel`: Menampilkan teks deskripsi.
- `JTextField` dan `JPasswordField`: Input untuk username dan password.
- `JButton`: Tombol untuk melakukan aksi login.

Validasi:
- Mengecek apakah username dan password cocok dengan nilai tertentu.
- Menampilkan dialog konfirmasi atau error menggunakan `JOptionPane`.

#  Implementasi Aplikasi Image Viewer

Program ini mengimplementasikan pembuatan aplikasi sederhana yang memungkinkan pengguna untuk membuka dan menampilkan gambar menggunakan JFileChooser.
```
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.File;

public class ImageViewer extends JFrame {
    private JLabel imageLabel;

    public ImageViewer() {
        // Mengatur judul frame
        setTitle("Image Viewer");
        setSize(600, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        // Panel utama
        JPanel panel = new JPanel();
        panel.setLayout(new BorderLayout());

        // Label untuk menampilkan gambar
        imageLabel = new JLabel("", SwingConstants.CENTER);
        panel.add(imageLabel, BorderLayout.CENTER);

        // Tombol untuk memilih gambar
        JButton openButton = new JButton("Open Image");
        panel.add(openButton, BorderLayout.SOUTH);

        // Tambahkan panel ke frame
        add(panel);

        // Listener untuk tombol open
        openButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                JFileChooser fileChooser = new JFileChooser();
                int result = fileChooser.showOpenDialog(null);

                if (result == JFileChooser.APPROVE_OPTION) {
                    File selectedFile = fileChooser.getSelectedFile();
                    ImageIcon imageIcon = new ImageIcon(selectedFile.getAbsolutePath());

                    // Mengatur ukuran gambar agar sesuai
                    Image img = imageIcon.getImage().getScaledInstance(imageLabel.getWidth(), imageLabel.getHeight(), Image.SCALE_SMOOTH);
                    imageLabel.setIcon(new ImageIcon(img));
                }
            }
        });
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            ImageViewer frame = new ImageViewer();
            frame.setVisible(true);
        });
    }
}
```

Komponen:
- `JLabel`: Untuk menampilkan gambar yang dipilih.
- `JButton`: Tombol untuk membuka file gambar.
- `JFileChooser`: Dialog untuk memilih file dari sistem.
Fitur:
- Gambar yang dipilih diatur ulang ukurannya agar pas dengan `JLabel`.
- Menggunakan `Image.SCALE_SMOOTH` untuk menghasilkan gambar berkualitas tinggi.
