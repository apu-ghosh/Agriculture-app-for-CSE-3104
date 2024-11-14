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
                string ins = "insert into user_info (Name,Division,District,Thana,Mobile,NID_number) values ('" + n + "','" + div + "','" + dist + "','" + th + "','" + m + "','" + nid + "')";
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

--------------- start Admin page ---------------------
public partial class admin_page : Window
{
    public admin_page()
    {
        InitializeComponent();
    }


    private void logout_button_Click(object sender, RoutedEventArgs e)
    {
        MainWindow mw = new MainWindow();
        mw.Show();
        this.Close();
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        home_page hp = new home_page();
        hp.Show();
        this.Close();
    }

    private void scheduling_button_Click(object sender, RoutedEventArgs e)
    {
        scheduling_page sp = new scheduling_page();
        sp.Show();
        this.Close();
    }

    private void instruction_button_Click(object sender, RoutedEventArgs e)
    {
        instruction_page ip = new instruction_page();
        ip.Show();
        this.Close();
    }

    // insert data in sql table--------------------
    private void insert_button_Click(object sender, RoutedEventArgs e)
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

        string sn = textbox1.Text;
        string cp = textbox2.Text;
        string td = textbox3.Text;
        string ft = textbox4.Text;


        try
        {
            if (insert_combobox.Text == "rice")
            {
                conn.Open();
                string ins = "insert into rice(Crop_Varieties_Name,Planting_Time,Type_of_Disease,Fertilizer_Application_time) values('" + sn + "','" + cp + "','" + td + "','" + ft + "')";
                MySqlCommand cmd = new MySqlCommand(ins, conn);
                int i = cmd.ExecuteNonQuery();
                MessageBox.Show("Data has inserted successfully...");

            }
            else if (insert_combobox.Text == "potato")
            {
                conn.Open();
                string ins = "insert into potato(Crop_Varieties_Name,Planting_Time,Type_of_Disease,Fertilizer_Application_time) values('" + sn + "','" + cp + "','" + td + "','" + ft + "')";
                MySqlCommand cmd = new MySqlCommand(ins, conn);
                int i = cmd.ExecuteNonQuery();
                MessageBox.Show("Data has inserted successfully...");

            }

            else
            {
                MessageBox.Show("Select Right Table");

            }

        }
        catch (Exception ex)
        {
            MessageBox.Show(ex.Message);
        }
        finally { conn.Close(); }


        insert_combobox.Text = "Select Table";
        textbox1.Text = "";
        textbox2.Text = "";
        textbox3.Text = "";
        textbox4.Text = "";
    }

    private void delete_button_Click(object sender, RoutedEventArgs e)
    {

        var a = (ComboBoxItem)delete_combobox_text.SelectedItem;
        string delete_data = (string)a.Content;
        string ddt = delet_data_text.Text;


        string s = "server= localhost; user= root; database= project3104; password =";
        MySqlConnection con = new MySqlConnection(s);

        if (delete_data == "user_info")
        {

            try
            {
                con.Open();
                MessageBox.Show("Successful");
                string del = "delete from user_info where User_Name = '" + ddt + "'";
                MySqlCommand cmd = new MySqlCommand(del, con);
                int i = cmd.ExecuteNonQuery();
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
            }

        }
        else if (delete_data == "potato")
        {
            try
            {
                con.Open();
                MessageBox.Show("Successful");
                string del = "delete from potato where Crop_Varieties_Name = '" + ddt + "'";
                MySqlCommand cmd = new MySqlCommand(del, con);
                int i = cmd.ExecuteNonQuery();
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
            }

        }
        else if (delete_data == "rice")
        {
            try
            {
                con.Open();
                MessageBox.Show("Successful");
                string del = "delete from rice where Crop_Varieties_Name = '" + ddt + "'";
                MySqlCommand cmd = new MySqlCommand(del, con);
                int i = cmd.ExecuteNonQuery();
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);
            }

        }
        else
        {
            con.Open();
            MessageBox.Show("Select your table ");
        }
       
        delet_data_text.Text = "";


    }

}




-----------------End Admin page ------------------





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
            else if (nid_number_box.Text == "apu123" && password_box.Text == "2024")
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
    private void login_button_Click(object sender, RoutedEventArgs e)
 {
     // Database connection string
     
     string pro = "server=localhost;user=root;database=project3104;password=";

     string un = user_name.Text;
     string pass = password.Text;

         using (MySqlConnection conn = new MySqlConnection(pro))
         {
             try
             {
                 conn.Open();
                
                 string query = "SELECT COUNT(*) FROM  user_info where User_Name='" + un + "' && password='" + pass + "'";
                 MySqlCommand cmdd = new MySqlCommand(query, conn);
                 cmdd.Parameters.AddWithValue("@user_name", user_name);
                 cmdd.Parameters.AddWithValue("@password", password); // In production, you should hash the password

                 int userCount = Convert.ToInt32(cmdd.ExecuteScalar());

                
                 if (userCount>0)
                 {
                
                   home_page hp = new home_page();
                    hp.Show();
                    this.Close();
                 }
                 else
                 {
                     MessageBox.Show("Invalid User_Name or password.", "Error");
                 }
             }
             catch (Exception ex)
             {
                 MessageBox.Show("Error: " + ex.Message);
             }
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

 
 ---------------instruction page----------------------

 public partial class instruction_page : Window
 {
     public instruction_page()
     {
         InitializeComponent();
     }

     private void back_button_Click(object sender, RoutedEventArgs e)
     {
         home_page hp = new home_page();
         hp.Show();
         this.Close();
     }

     private void Button_Click(object sender, RoutedEventArgs e)
     {
        MainWindow mw = new MainWindow();
         mw.Show();
         this.Close();
     }

 var a = (ComboBoxItem)select_itembox.SelectedItem;
 string table_name = (string)a.Content;

 // Connection string
 string connectionString = "server=localhost;user=root;database=project3104;password=";
 using (MySqlConnection con = new MySqlConnection(connectionString))
     try
     {


         if (table_name == "rice")
         {
             con.Open();

             // Query to fetch all data from the selected table
             string query = "SELECT * FROM rice";

             using (MySqlCommand cmd = new MySqlCommand(query, con))
             using (MySqlDataAdapter adapter = new MySqlDataAdapter(cmd))
             {
                 // Load data into a DataTable
                 DataTable dataTable = new DataTable();
                 adapter.Fill(dataTable);

                 // Bind the DataTable to the DataGridView
                 dataGridView1.ItemsSource = dataTable.DefaultView;
                 con.Close();
             }


         }

         else if (table_name == "potato")
         {

             // Query to fetch all data from the selected table
             string query = "SELECT * FROM potato";

             using (MySqlCommand cmd = new MySqlCommand(query, con))
             using (MySqlDataAdapter adapter = new MySqlDataAdapter(cmd))
             {
                 // Load data into a DataTable
                 DataTable dataTable = new DataTable();
                 adapter.Fill(dataTable);

                 // Bind the DataTable to the DataGridView
                 dataGridView1.ItemsSource = dataTable.DefaultView;
                 con.Close();
             }


         }
         else
         {
             MessageBox.Show("Please select a valid table name.");
             return;
         }


     }
     catch (Exception ex)
     {
         MessageBox.Show($"An error occurred: {ex.Message}");
     }
     }

     private void data_clear_button_Click(object sender, RoutedEventArgs e)
     {
         dataGridView1.ItemsSource = "";
         select_itembox.Text = "";
     }
 }
-------------------------end instruction page------------------------------
