# Agriculture-app-for-CSE-3104
Agriculture app
-----------------sign up page-----------------
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Shapes;

using MySql.Data.MySqlClient;



namespace Agriculture_app
{
    /// <summary>
    /// Interaction logic for sign_up.xaml
    /// </summary>
    public partial class sign_up : Window
    {
        public sign_up()
        {
            InitializeComponent();
        }

        
        private void submit_button_Click(object sender, RoutedEventArgs e)
        {
            string pro = "server=localhost;user=root;database=project3104;password=";
            MySqlConnection conn = new MySqlConnection(pro);
            try
            {

                conn.Open();
                MessageBox.Show("Successful");
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
            }
            finally { conn.Close(); }

            string n = name.Text;
            
            string div = division.Text;
            string dist = district.Text;
            
            string th = thana.Text;
            

            int m = Int32.Parse(mobile.Text);
            int nid = Int32.Parse(nid_number.Text);

            try
            {
               // string ss = "server=localhost; user=root; database=project3104; password =";

                conn.Open();
                string ins = "insert into farmer_info (Name,Division,District,Thana,Mobile,NID_number) values ('" + n + "','" + div + "','" + dist + "','" + th + "','" + m + "','" + nid + "')";
                MySqlCommand cmd = new MySqlCommand(ins, conn);
                int i = cmd.ExecuteNonQuery();
                MessageBox.Show("Data has inserted successfully...");
            }
      
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
            }
            finally { conn.Close(); }

            home_page hm = new home_page();
            hm.Show();
            this.Close();

        }

        private void back_button_Click(object sender, RoutedEventArgs e)
        {
            MainWindow mw = new MainWindow();
            mw.Show();
            this.Close();
        }
    }
}

-----------------sign up page end-----------------




---------------main window-----------------------

public partial class MainWindow : Window
{
    string pro = "server=localhost;user=root;database=project3104;password=";
    public MainWindow()
    {
        
        InitializeComponent();
    }
    
  
    private void sign_up_button_Click(object sender, RoutedEventArgs e)
    {
        sign_up su = new sign_up();
        su.Show();
        this.Close();
    }

    private void admin_buttion_Click(object sender, RoutedEventArgs e)
    {
        
            if (nid_number_box.Text == "" && password_box.Text == " ")
            {
                MessageBox.Show("Missing Information");
            }
            else if (nid_number_box.Text == "12345678" && password_box.Text == "2024")
            {
                admin_page ap = new admin_page();
                ap.Show();
                this.Close();
            }
            else
            {
                MessageBox.Show("Please Enter The Correct  Username And Password");
            }
        
    }
}





-----------------end main window----------------------



-----------------home page----------------------------

public partial class home_page : Window
 {
     public home_page()
     {
         InitializeComponent();
     }

     private void logout_Click(object sender, RoutedEventArgs e)
     {
         MainWindow mw = new MainWindow();
         mw.Show();
         this.Close();
     }

     private void button_1_Click(object sender, RoutedEventArgs e)
     {
         
         scheduling_page sp = new scheduling_page();
         sp.Show();
         this.Close();   
     }

     private void button_3_Click(object sender, RoutedEventArgs e)
     {
         instruction_page ip = new instruction_page();
         ip.Show();
         this.Close();
     }
 }
 ----------------end home page-=----------------------
 
