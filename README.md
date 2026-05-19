import streamlit as st
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.preprocessing import StandardScaler

# Cấu hình trang web
st.set_page_config(page_title="Hệ thống Chấm bài ITA106", layout="wide")
st.title("📊 Hệ thống Nộp bài và Xử lý Dữ liệu tự động (ITA106)")
st.write("Hãy tải file dữ liệu của bạn lên (định dạng .csv hoặc .xlsx) để hệ thống tự động xử lý 4 bài tập.")

# Khu vực upload file
uploaded_file = st.file_uploader("Chọn file dữ liệu", type=["csv", "xlsx"])

if uploaded_file is not None:
    # Đọc dữ liệu
    try:
        if uploaded_file.name.endswith('.csv'):
            df = pd.read_csv(uploaded_file)
        else:
            df = pd.read_excel(uploaded_file)
        st.success("Tải dữ liệu lên thành công!")
    except Exception as e:
        st.error(f"Lỗi khi đọc file: {e}")
        st.stop()

   # Tạo các Tab tương ứng với 4 bài tập
  tab1, tab2, tab3, tab4 = st.tabs(["Bài 1: Khám phá", "Bài 2: Làm sạch", "Bài 3: Outliers", "Bài 4: Sơ đồ quy trình"])

  # ==========================================
  # BÀI 1: KHÁM PHÁ DỮ LIỆU BAN ĐẦU
 # ==========================================
  with tab1:
        st.header("Bài 1: Khám phá dữ liệu ban đầu (2đ)")
        
  st.subheader("1. Hiển thị 10 dòng dữ liệu đầu tiên")
        st.dataframe(df.head(10))
        
 st.subheader("2. Kiểm tra số lượng bản ghi và thuộc tính")
        st.write(f"- Số lượng bản ghi (dòng): **{df.shape[0]}**")
        st.write(f"- Số lượng thuộc tính (cột): **{df.shape[1]}**")
        
 st.subheader("3. Kiểm tra kiểu dữ liệu của từng cột")
        dtype_df = pd.DataFrame(df.dtypes, columns=["Kiểu dữ liệu"]).astype(str)
        st.dataframe(dtype_df)
        
  st.subheader("4. Tính toán các thống kê cơ bản")
        st.write("Bao gồm: Giá trị trung bình, Max, Min, Độ lệch chuẩn (chỉ áp dụng cho cột số)")
        st.dataframe(df.describe().T[['mean', 'max', 'min', 'std']])
        
 st.subheader("5. Trực quan hóa dữ liệu bằng các biểu đồ")
        num_cols = df.select_dtypes(include=[np.number]).columns.tolist()
        cat_cols = df.select_dtypes(exclude=[np.number]).columns.tolist()
        
 col1, col2 = st.columns(2)
        with col1:
            st.write("**Histogram cho các thuộc tính số:**")
            if num_cols:
                selected_num = st.selectbox("Chọn cột số để vẽ Histogram", num_cols, key="hist")
                fig, ax = plt.subplots()
                sns.histplot(df[selected_num].dropna(), kde=True, ax=ax, color='skyblue')
                st.pyplot(fig)
            else:
                st.warning("Không có thuộc tính số nào.")
                
  with col2:
            st.write("**Bar chart cho các thuộc tính phân loại:**")
            if cat_cols:
                selected_cat = st.selectbox("Chọn cột phân loại để vẽ Bar chart", cat_cols, key="bar")
                fig, ax = plt.subplots()
                # Giới hạn top 10 giá trị phổ biến nhất để tránh rối biểu đồ
                df[selected_cat].value_counts().head(10).plot(kind='bar', ax=ax, color='salmon')
                plt.xticks(rotation=45)
                st.pyplot(fig)
            else:
                st.warning("Không có thuộc tính phân loại nào.")

   # ==========================================
  # BÀI 2: LÀM SẠCH DỮ LIỆU
  # ==========================================
 with tab2:
        st.header("Bài 2: Làm sạch dữ liệu (2đ)")
        
  st.subheader("1. Kiểm tra dữ liệu bị thiếu (Missing Values)")
        missing_count = df.isnull().sum()
        st.dataframe(pd.DataFrame(missing_count, columns=["Số lượng giá trị thiếu"]))
        
  st.subheader("2. Xử lý dữ liệu thiếu và trùng lặp")
        method = st.radio("Chọn phương pháp xử lý dữ liệu thiếu:", 
                          ("Giữ nguyên để test", "Xóa bản ghi chứa giá trị thiếu", "Điền giá trị trung bình/trung vị (cho cột số)"))
        
  df_cleaned = df.copy()
        if method == "Xóa bản ghi chứa giá trị thiếu":
            df_cleaned = df_cleaned.dropna()
            st.caption(f"Đã xóa. Số bản ghi còn lại: {df_cleaned.shape[0]}")
        elif method == "Điền giá trị trung bình/trung vị (cho cột số)":
            for col in num_cols:
                df_cleaned[col] = df_cleaned[col].fillna(df_cleaned[col].median())
            st.caption("Đã điền giá trị Trung vị (Median) vào các cột số bị thiếu.")
            
  # Loại bỏ trùng lặp
  dup_count = df_cleaned.duplicated().sum()
        st.write(f"- Phát hiện số bản ghi trùng lặp: **{dup_count}**")
        if dup_count > 0:
            df_cleaned = df_cleaned.drop_duplicates()
            st.success("Đã loại bỏ các bản ghi trùng lặp!")

 st.subheader("3. Chuẩn hóa dữ liệu số (Standardization)")
        if num_cols:
            scaler = StandardScaler()
            df_scaled = df_cleaned.copy()
            df_scaled[num_cols] = scaler.fit_transform(df_cleaned[num_cols].fillna(0)) # Điền tạm 0 để scale nếu chưa xử lý hết
            st.write("Dữ liệu sau khi Chuẩn hóa (Z-score Standardization) 5 dòng đầu:")
            st.dataframe(df_scaled[num_cols].head())
        
st.subheader("4. Vẽ Boxplot so sánh TRƯỚC và SAU khi làm sạch")
        if num_cols:
            selected_box = st.selectbox("Chọn cột số để so sánh Boxplot", num_cols, key="box_clean")
            fig, axes = plt.subplots(1, 2, figsize=(10, 4))
            sns.boxplot(y=df[selected_box], ax=axes[0], color='lightcoral')
            axes[0].set_title("Trước khi làm sạch (Ban đầu)")
            
 sns.boxplot(y=df_cleaned[selected_box], ax=axes[1], color='lightgreen')
            axes[1].set_title("Sau khi làm sạch/Xử lý thiếu")
            st.pyplot(fig)

 # ==========================================
  # BÀI 3: PHÁT HIỆN OUTLIERS
 # ==========================================
 with tab3:
        st.header("Bài 3: Phát hiện Outliers trong dữ liệu (2đ)")
        if num_cols:
            col_outlier = st.selectbox("Chọn cột số cần phân tích Outliers", num_cols, key="outlier_col")
            
   # Tính IQR
   Q1 = df_cleaned[col_outlier].quantile(0.25)
            Q3 = df_cleaned[col_outlier].quantile(0.75)
            IQR = Q3 - Q1
            lower_bound = Q1 - 1.5 * IQR
            upper_bound = Q3 + 1.5 * IQR
            outliers_iqr = df_cleaned[(df_cleaned[col_outlier] < lower_bound) | (df_cleaned[col_outlier] > upper_bound)]
            
 # Tính Z-score
 mean_val = df_cleaned[col_outlier].mean()
            std_val = df_cleaned[col_outlier].std()
            z_scores = (df_cleaned[col_outlier] - mean_val) / std_val
            outliers_z = df_cleaned[np.abs(z_scores) > 3]
            
 st.subheader("1. Kết quả áp dụng phương pháp IQR & Z-score")
            st.write(f"- **Phương pháp IQR:** Phát hiện **{len(outliers_iqr)}** dòng dữ liệu ngoại lai.")
            st.write(f"- **Phương pháp Z-score (ngưỡng |z| > 3):** Phát hiện **{len(outliers_z)}** dòng dữ liệu bất thường.")
            
 st.subheader("2. Vẽ biểu đồ phân tích")
            col_b3_1, col_b3_2 = st.columns(2)
            with col_b3_1:
                st.write("**Boxplot phát hiện dị biệt:**")
                fig, ax = plt.subplots()
                sns.boxplot(x=df_cleaned[col_outlier], ax=ax, color='gold')
                st.pyplot(fig)
            with col_b3_2:
                st.write("**Scatter Plot (Biểu đồ phân tán):**")
                if len(num_cols) > 1:
                    # Chọn thêm 1 cột nữa để vẽ scatter
                    other_cols = [c for c in num_cols if c != col_outlier]
                    y_axis = st.selectbox("Chọn trục Y cho Scatter plot", other_cols)
                    fig, ax = plt.subplots()
                    sns.scatterplot(data=df_cleaned, x=col_outlier, y=y_axis, ax=ax, color='purple')
                    st.pyplot(fig)
                else:
                    st.info("Cần ít nhất 2 cột số để vẽ Scatter Plot.")
                    
  st.subheader("3. Phân tích ảnh hưởng của Outliers đối với mô hình Học máy")
            st.info("""
            > **💡 Đánh giá lý thuyết:**
            > * **Thuật toán nhạy cảm với Outliers:** Các mô hình tuyến tính (Linear/Logistic Regression), K-Means, KNN sẽ bị lệch nghiêm trọng do Outliers làm thay đổi khoảng cách và hàm mất mát (MSE).
            > * **Thuật toán ít nhạy cảm:** Các mô hình dựa trên cây quyết định (Decision Tree, Random Forest, XGBoost) xử lý dữ liệu dựa trên việc phân ngưỡng (split), do đó ít bị ảnh hưởng bởi giá trị cực đoan hơn.
            """)
        else:
            st.warning("Vui lòng tải dữ liệu có chứa cột số để phân tích Outliers.")
 # ==========================================
 # BÀI 4: THIẾT KẾ SƠ ĐỒ QUY TRÌNH
  # ==========================================
 with tab4:
        st.header("Bài 4: Thiết kế sơ đồ thể hiện các bước (2đ)")
        st.write("Sơ đồ luồng xử lý dữ liệu chuẩn trong Khoa học dữ liệu (Data Science Pipeline):")
        
   # Tạo sơ đồ trực quan bằng Markdown / HTML kiểu Graph
 st.markdown("""
        <div style="background-color: #f0f2f6; padding: 20px; border-radius: 10px; font-family: sans-serif;">
            <div style="text-align: center; font-weight: bold; padding: 10px; background: #ff4b4b; color: white; border-radius: 5px; margin-bottom: 10px;">
                1. THU THẬP DỮ LIỆU (Data Collection)
            </div>
            <div style="text-align: center; font-size: 20px;">⬇️</div>
            <div style="text-align: center; font-weight: bold; padding: 10px; background: #00a65a; color: white; border-radius: 5px; margin-bottom: 10px;">
                2. LÀM SẠCH DỮ LIỆU (Data Cleaning) <br><small>(Xử lý missing, loại trùng, chuẩn hóa, sửa lỗi)</small>
            </div>
            <div style="text-align: center; font-size: 20px;">⬇️</div>
            <div style="text-align: center; font-weight: bold; padding: 10px; background: #00c0ef; color: white; border-radius: 5px; margin-bottom: 10px;">
                3. KHÁM PHÁ DỮ LIỆU (EDA) <br><small>(Thống kê, vẽ biểu đồ Histogram, Bar chart, tìm insight)</small>
            </div>
            <div style="text-align: center; font-size: 20px;">⬇️</div>
            <div style="text-align: center; font-weight: bold; padding: 10px; background: #f39c12; color: white; border-radius: 5px; margin-bottom: 10px;">
                4. TRÍCH XUẤT ĐẶC TRƯNG (Feature Engineering) <br><small>(Mã hóa, chọn lọc biến, tạo biến mới)</small>
            </div>
            <div style="text-align: center; font-size: 20px;">⬇️</div>
            <div style="text-align: center; font-weight: bold; padding: 10px; background: #605ca8; color: white; border-radius: 5px; margin-bottom: 10px;">
                5. HUẤN LUYỆN MÔ HÌNH (Model Training) <br><small>(Lựa chọn thuật toán và fit dữ liệu)</small>
            </div>
            <div style="text-align: center; font-size: 20px;">⬇️</div>
            <div style="text-align: center; font-weight: bold; padding: 10px; background: #3c8dbc; color: white; border-radius: 5px;">
                6. ĐÁNH GIÁ MÔ HÌNH (Model Evaluation) <br><small>(Tính toán Accuracy, R2 score, MSE, MAE,...)</small>
            </div>
        </div>
        """, unsafe_allow_html=True)
