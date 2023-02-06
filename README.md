# MINI-PROJECT-1---TACH-ANH-MAU-RGB
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace MP1___TACH_ANH_MAU_RGB
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();

            // Tạo một biến chứa đường dẫn - nơi lưu trữ hình ảnh màu RGB gốc cần xử lý
            string filehinh = @"C:\Users\ADMIN\Pictures\co gai Lena.jpg";

            // Tạo một biến chứa hình bitmap (1 loạt chấm pixel) được load từ filehinh trên
            Bitmap hinhgoc = new Bitmap(filehinh);

            // Hiển thị hình gốc trong picBox_HinhGoc đã tạo 
            picBox_HinhGoc.Image = hinhgoc;

            // Khai báo 3 hình bitmap RGB cho 3 kênh RED-GREEN-BLUE
            //Bitmap(Int32, Int32) - Khởi tạo một phiên bản mới của lớp Bitmap với kích thước được chỉ định.
            Bitmap red = new Bitmap(hinhgoc.Width, hinhgoc.Height);
            Bitmap green = new Bitmap(hinhgoc.Width, hinhgoc.Height);
            Bitmap blue = new Bitmap(hinhgoc.Width, hinhgoc.Height);
            
            // Mỗi hình là một ma trận hai chiều nên ta sử dụng 2 vòng for để quét hết điểm ảnh trong hình 
            for(int x = 0; x < hinhgoc.Width; x++) // for quét chiều ngang
                for(int y = 0; y < hinhgoc.Height; y++) // for quét chiều dọc
                {
                    // Đọc giá trị pixel tại điểm ảnh có vị trí (x,y), giá trị pixel này nằm trong kiểu dữ liệu Color của C#
                    // Giá trị pixel trả về sẽ nằm trong một kiểu dữ liệu Color
                    Color pixel = hinhgoc.GetPixel(x, y);
                    // Color của C# là một cấu trúc chứa dữ liệu 4 thành phần red, green, blue và độ trong suốt A
                    // Nhờ đó trích xuất được các giá trị ảnh màu tại những điểm x, y vị trí đang xét
                    // Mỗi giá trị kênh màu chiếm 1 byte 
                    byte R = pixel.R; // Khai báo biến byte - vì mỗi giá trị kênh màu là 1 byte từ 0 đến 256 giá trị cụ thể
                    byte G = pixel.G;
                    byte B = pixel.B;
                    byte A = pixel.A;

                    // Set các giá trị pixel đọc được trong các hình ảnh 
                    // Các kênh màu tương ứng R, G, B
                    red.SetPixel(x, y, Color.FromArgb(A, R, 0, 0)); // RED thực chất là 1 ảnh màu  - nên cũng có 3 kênh
                    green.SetPixel(x, y, Color.FromArgb(A, 0, G, 0));
                    blue.SetPixel(x, y, Color.FromArgb(A, 0, 0, B));

                }
            // Hiển thị 3 hình kênh màu R-G-B tại các điểm picBox đã tạo
            picBox_RED.Image = red;
            picBox_GREEN.Image = green;
            picBox_BLUE.Image = blue;

           
        }
    }
}
