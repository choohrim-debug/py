import os
import pandas as pd
import matplotlib.pyplot as plt

# 1. 데이터 불러오기
csv_file = '전력수요.csv'
if not os.path.exists(csv_file):
    print(f"Error: {csv_file} 파일을 찾을 수 없습니다. 저장소 루트에 추가해주세요.")
    exit(1)

df = pd.read_csv(csv_file)

# 2. 데이터 전처리 (날짜 변환 및 인덱스 설정)
df['일시'] = pd.to_datetime(df['일시'])
df.set_index('일시', inplace=True)

# 시간별 데이터는 양이 많아 선이 뭉쳐 보일 수 있으므로 일별 평균(Daily Mean) 데이터로 변환합니다.
daily_df = df.resample('D').mean()

# 3. 그래프 그리기 (GitHub Actions 환경을 위해 레이블은 영어로 작성)
fig, ax = plt.subplots(figsize=(12, 6))
ax.plot(daily_df.index, daily_df['전력수요(MWh)'], label='Daily Average Demand (MWh)', color='#1f77b4', linewidth=2)

# 그래프 스타일 수정
ax.set_title('Electricity Demand Trends (2025)', fontsize=16, fontweight='bold', pad=15)
ax.set_xlabel('Date', fontsize=12, labelpad=10)
ax.set_ylabel('Power Demand (MWh)', fontsize=12, labelpad=10)
ax.grid(True, linestyle='--', alpha=0.5)
ax.legend(loc='upper right', fontsize=11)

plt.tight_layout()

# 4. 이미지 저장 (DPI 설정을 높여 고화질로 저장)
output_image = 'power_demand_visualization.png'
plt.savefig(output_image, dpi=300)
print(f"시각화 완료: {output_image} 파일이 정상적으로 생성되었습니다.")
