# Image-Resizer-Tool
import os
from PIL import Image
input_folder = "input_images"          
output_folder = "output_images"       
new_width = 800                       
new_height = 800                      
convert_format = "JPEG"                Change to "PNG", "WEBP", etc., or None to disable conversion
def resize_and_convert():
    if not os.path.exists(output_folder):
        os.makedirs(output_folder)
    for filename in os.listdir(input_folder):
        file_path = os.path.join(input_folder, filename)
        if not filename.lower().endswith((".jpg", ".jpeg", ".png", ".webp", ".bmp", ".gif")):
            continue
        img = Image.open(file_path)
        img_resized = img.resize((new_width, new_height))
        base_name, _ = os.path.splitext(filename)
        if convert_format:
            output_file = os.path.join(output_folder, f"{base_name}.{convert_format.lower()}")
            img_resized.save(output_file, convert_format)
        else:
            output_file = os.path.join(output_folder, filename)
            img_resized.save(output_file)
        print(f"Processed: {filename} → {output_file}")
    print("\nAll images resized successfully!")
if __name__ == "__main__":
    resize_and_convert()
    
