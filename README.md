# COMPATIBILITY-ASSESSMENT-TEST-FOR-BACKEND-
using System;
using System.Data;
using System.Windows.Forms;
using System.Data.SqlClient;

namespace Inventory
{
    using System;
    using System.Collections;

    class Inventory
    {
        String name;
        double Cost;
        int Price;

    }
    public Inventory (string n, double c, int h)

    
        //Insert Data  
        private void btn_Insert_Click(object sender, EventArgs e)
        {
            if (txt_Name.Text != "" && txt_State.Text != "")
            {
                cmd = new SqlCommand("insert into tbl_Record(Name,Price) values(@name,@Price)", con);
                con.Open();
                cmd.Parameters.AddWithValue("@name", txt_Name.Text);
                cmd.Parameters.AddWithValue("@Price", int_Price.Text);
                cmd.ExecuteNonQuery();
                con.Close();
                MessageBox.Show("Record Inserted Successfully");
                DisplayData();
                ClearData();
            }
            else
            {
                MessageBox.Show("Please Provide Details!");
            }
        }
        //Display Data in DataGridView  
        private void DisplayData()
        {
            con.Open();
            DataTable dt = new DataTable();
            adapt = new SqlDataAdapter("select * from tbl_Record", con);
            adapt.Fill(dt);
            dataGridView1.DataSource = dt;
            con.Close();
        }
        //Clear Data  
        private void ClearData()
        {
            txt_Name.Text = "";
            int_Price.int = "";
            ID = 0;
        }
        //dataGridView1 RowHeaderMouseClick Event  
        private void dataGridView1_RowHeaderMouseClick(object sender, DataGridViewCellMouseEventArgs e)
        {
            ID = Convert.ToInt32(dataGridView1.Rows[e.RowIndex].Cells[0].Value.ToString());
            txt_Name.Text = dataGridView1.Rows[e.RowIndex].Cells[1].Value.ToString();
            int_Price.int = dataGridView1.Rows[e.RowIndex].Cells[2].Value.ToString();
        }
        //Update Record  
        private void btn_Update_Click(object sender, EventArgs e)
        {
            if (txt_Name.Text != "" && int_Price.int != "")
            {
                cmd = new SqlCommand("update tbl_Record set Name=@name,Price=@price where ID=@id", con);
                con.Open();
                cmd.Parameters.AddWithValue("@id", ID);
                cmd.Parameters.AddWithValue("@name", txt_Name.Text);
                cmd.Parameters.AddWithValue("@price", int_Price.int);
                cmd.ExecuteNonQuery();
                MessageBox.Show("Record Updated Successfully");
                con.Close();
                DisplayData();
                ClearData();
            }
            else
            {
                MessageBox.Show("Please Select Record to Update");
            }
        }
        //Delete Record  
        private void btn_Delete_Click(object sender, EventArgs e)
        {
            if (ID != 0)
            {
                cmd = new SqlCommand("delete tbl_Record where ID=@id", con);
                con.Open();
                cmd.Parameters.AddWithValue("@id", ID);
                cmd.ExecuteNonQuery();
                con.Close();
                MessageBox.Show("Record Deleted Successfully!");
                DisplayData();
                ClearData();
            }
            else
            {
                MessageBox.Show("Please Select Record to Delete");
            }
        }
    }
}
namespace Inventory
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
