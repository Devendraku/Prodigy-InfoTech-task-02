# Prodigy-InfoTech-task-02
 Python program that implements a simple image encryption tool using pixel manipulation. It performs XOR operation on the RGB values of each pixel to encrypt and decrypt the image:

 from PIL import Image

def encrypt_image(image_path, key):
    # Open the image
    img = Image.open(image_path)
    width, height = img.size
    
    # Convert image to RGB mode
    img = img.convert('RGB')
    
    # Create a new image to store the encrypted pixels
    encrypted_img = Image.new('RGB', (width, height))
    
    # Loop through each pixel in the image
    for x in range(width):
        for y in range(height):
            r, g, b = img.getpixel((x, y))
            r = (r + key) % 256  # Encrypting red channel
            g = (g + key) % 256  # Encrypting green channel
            b = (b + key) % 256  # Encrypting blue channel
            encrypted_img.putpixel((x, y), (r, g, b))
    
    # Save the encrypted image
    encrypted_img.save("encrypted_image.png")
    print("Image encrypted successfully.")

def decrypt_image(image_path, key):
    # Open the encrypted image
    encrypted_img = Image.open(image_path)
    width, height = encrypted_img.size
    
    # Create a new image to store the decrypted pixels
    decrypted_img = Image.new('RGB', (width, height))
    
    # Loop through each pixel in the image
    for x in range(width):
        for y in range(height):
            r, g, b = encrypted_img.getpixel((x, y))
            r = (r - key) % 256  # Decrypting red channel
            g = (g - key) % 256  # Decrypting green channel
            b = (b - key) % 256  # Decrypting blue channel
            decrypted_img.putpixel((x, y), (r, g, b))
    
    # Save the decrypted image
    decrypted_img.save("decrypted_image.png")
    print("Image decrypted successfully.")

def main():
    while True:
        choice = input("Do you want to encrypt or decrypt an image? (encrypt/decrypt/exit): ").lower()
        if choice == 'exit':
            break
        elif choice == 'encrypt':
            image_path = input("Enter the path to the image you want to encrypt: ")
            key = int(input("Enter the encryption key (an integer): "))
            encrypt_image(image_path, key)
        elif choice == 'decrypt':
            image_path = input("Enter the path to the image you want to decrypt: ")
            key = int(input("Enter the decryption key (an integer): "))
            decrypt_image(image_path, key)
        else:
            print("Invalid choice. Please enter 'encrypt', 'decrypt', or 'exit'.")

if __name__ == "__main__":
    main()

