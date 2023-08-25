# MANIPULA-O_PDF
from PIL import Image
import os

pasta = input("Cole o caminho onde estão suas pastas:")
caminho = input('Cole o caminho onde quer que salve os pdf:')

def images_to_pdf(image_folder, output_pdf_path):
    # Lista para armazenar imagens
    images_list = []
    
    # Carregue todas as imagens da pasta
    for image_file in sorted(os.listdir(image_folder)):
        if image_file.lower().endswith(('.png', '.jpg', '.jpeg')):
            image_path = os.path.join(image_folder, image_file)
            with Image.open(image_path) as im:
                images_list.append(im.convert('RGB'))
    
    # Salve as imagens como um único PDF
    if images_list:
        images_list[0].save(output_pdf_path, save_all=True, append_images=images_list[1:])

# Pasta principal
source_directory = pasta
destination_directory = caminho

# Para cada subpasta em source_directory
for folder_name in os.listdir(source_directory):
    folder_path = os.path.join(source_directory, folder_name)
    
    # Verifique se é realmente uma pasta
    if os.path.isdir(folder_path):
        output_pdf_name = folder_name + ".pdf"
        output_pdf_path = os.path.join(destination_directory, output_pdf_name)
        
        # Concatene as imagens dessa subpasta
        images_to_pdf(folder_path, output_pdf_path)

print("CONCATENADO")
