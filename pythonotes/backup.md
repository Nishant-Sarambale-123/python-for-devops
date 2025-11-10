import shutil
from datetime import datetime

source = "/home/ubuntu/mydata"
backup_dir = "/home/ubuntu/backups"

current_time = datetime.now().strftime("%Y-%m-%d_%H-%M-%S")
zip_filename = f"{backup_dir}/backup_{current_time}"

shutil.make_archive(zip_filename, 'zip', source)

print(f"✅ Backup created successfully at: {zip_filename}.zip")
