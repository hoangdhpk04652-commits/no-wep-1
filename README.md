import streamlit as st
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import sys
import io

# Cấu hình giao diện
st.set_page_config(page_title="Hệ thống chấm bài ITA106", layout="wide")

st.title("🖥️ Trình Thực Thi Code Python - Nộp Bài ITA106")
st.write("Dán đoạn code Python của bạn vào ô dưới đây, sau đó bấm **'Chạy Code'** để xem kết quả hiển thị.")

# Tạo bố cục 2 cột: Cột trái nhập code, Cột phải hiển thị kết quả
col_code, col_result = st.columns([1, 1])

with col_code:
    st.subheader("📝 Khu vực dán mã nguồn (Code)")
    
    # Đoạn code mẫu mặc định sẵn trong ô để người dùng dễ hình dung
    default_code = """# Hãy viết hoặc dán code bài làm của bạn vào đây
import pandas as pd
import numpy as np

# 1. Tạo dữ liệu giả lập để test
data = {
    'Tuổi': [25, 30, 35, np.nan, 40, 28, 35, 150, 32, 30], # 150 là outlier
    'Thu_Nhap': [10, 15, 20, 25, 30, 15, 20, 25, 22, 15],
    'Loai_Khach': ['VIP', 'Normal', 'VIP', 'Normal', 'VIP', 'Normal', 'Normal', 'VIP', 'Normal', 'Normal']
}
df = pd.DataFrame(data)

# ---- BÀI 1: KHÁM PHÁ DỮ LIỆU ----
print("--- 10 DÒNG DỮ LIỆU ĐẦU TIÊN ---")
print(df.head(10))

print("\\n--- SỐ LƯỢNG BẢN GHI VÀ THUỘC TÍNH ---")
print(f"Số dòng: {df.shape[0]}, Số cột: {df.shape[1]}")

print("\\n--- THỐNG KÊ CƠ BẢN ---")
print(df.describe())
"""

    # Ô nhập liệu Code
    user_code = st.text_area(
        "Nhập code Python của bạn tại đây:", 
        value=default_code, 
        height=450,
        help="Hỗ trợ các thư viện pandas, numpy, matplotlib, seaborn, sklearn..."
    )
    
    # Nút bấm kích hoạt chạy code
    run_button = st.button("🚀 CHẠY CODE BÀI LÀM", type="primary", use_container_width=True)

with col_result:
    st.subheader("📺 Kết quả đầu ra (Output)")
    
    if run_button:
        # Tạo khu vực bắt dữ liệu xuất ra từ lệnh print()
        old_stdout = sys.stdout
        redirected_output = sys.stdout = io.StringIO()
        
        # Xóa các hình vẽ cũ tránh bị đè hình
        plt.clf()
        plt.close('all')
        
        try:
            st.info("🔄 Hệ thống đang biên dịch và chạy code...")
            
            # Thực thi đoạn code của người dùng trong môi trường an toàn (sandbox-like)
            # Cho phép sử dụng các biến toàn cục cần thiết
            exec_globals = {
                'pd': pd,
                'np': np,
                'plt': plt,
                'sns': sns,
                'st': st # Cho phép người dùng dùng lệnh st.write() nếu họ biết
            }
            
            exec(user_code, exec_globals)
            
            # Lấy các chuỗi ký tự xuất ra từ lệnh print() trong code
            sys.stdout = old_stdout
            output_text = redirected_output.getvalue()
            
            # Hiển thị kết quả dạng Text (từ các lệnh print)
            if output_text:
                st.code(output_text, language="text")
            else:
                st.caption("Code chạy thành công nhưng không có lệnh print() nào để xuất văn bản.")
                
            # TỰ ĐỘNG BẮT BIỂU ĐỒ: Nếu trong code của người dùng có vẽ hình (plt.show() hoặc vẽ bằng seaborn)
            if plt.get_fignums():
                st.write("**📊 Biểu đồ được sinh ra từ code:**")
                st.pyplot(plt.gcf())
                
            st.success("✅ Đã chạy xong!")
            
        except Exception as e:
            # Nếu code của người dùng bị lỗi cú pháp hoặc lỗi logic, bắt lỗi và hiển thị lên màn hình
            sys.stdout = old_stdout
            st.error(f"❌ Lỗi Code hệ thống không chạy được:\n{e}")
    else:
        st.write("Chưa có dữ liệu. Hãy bấm nút **'Chạy Code'** ở cột bên trái.")
