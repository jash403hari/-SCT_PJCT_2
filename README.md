# SCT_PJCT_2
# === IMAGE ENCRYPTION & DECRYPTION ===
# This program encrypts and decrypts an image using XOR operation.

       from PIL import Image
        import os

# === IMAGE LOADING ===
# Define the absolute path of the image (Change this to your actual image path)
        image_path = r"C:\Users\jash4\Pictures\proj\ZC2OBFD.jpg"

# Debugging: Check if file exists before proceeding
        if not os.path.exists(image_path):
        print("File not found at:", image_path)
    else:
        image = Image.open(image_path)  # Open the image
        image.show()  # Display the original image
        print("Done! Image loaded and displayed successfully.")


# === IMAGE ENCRYPTION ===
# Define the encryption key (Choose any integer value)
        key = 123  

# Function to Encrypt Image using XOR
        def encrypt_image(image, key):
 """
    Encrypts an image using XOR bitwise operation.

  Parameters:
    - image (PIL Image): The input image to encrypt.
    - key (int): Encryption key.

   Returns:
    - PIL Image: Encrypted image.
    """
    pixels = list(image.getdata())  # Get all pixels
    new_pixels = []

   # Apply XOR operation to each pixel value
     for pixel in pixels:
        new_pixel = tuple((value ^ key) for value in pixel)  # XOR each pixel component
         new_pixels.append(new_pixel)

  # Create new image with modified pixels
        new_image = Image.new(image.mode, image.size)
        new_image.putdata(new_pixels)
        return new_image

# Check if image exists before encrypting
if os.path.exists(image_path):
    image = Image.open(image_path)  # Load image
    print("Original image loaded successfully.")

        # Encrypt Image
        encrypted_image = encrypt_image(image, key)
        encrypted_image.save("encrypted_image.png")  # Save encrypted image
        encrypted_image.show()  # Display encrypted image
        print("Encryption completed. Encrypted image saved as 'encrypted_image.png'.")
    else:
        print("Error: Original image not found!")


# === IMAGE DECRYPTION ===
# Define the path of the encrypted image
        encrypted_image_path = "encrypted_image.png"

# Function to Decrypt Image using XOR (Same logic as encryption)
    def decrypt_image(image, key):
  """
    Decrypts an image using XOR bitwise operation (same function as encryption).

   Parameters:
    - image (PIL Image): The encrypted image to decrypt.
    - key (int): Encryption key (must be same as used for encryption).

  Returns:
    - PIL Image: Decrypted image.
    """
    pixels = list(image.getdata())  # Get all pixels
    new_pixels = []

  # Apply XOR operation again (Reverses encryption)
    for pixel in pixels:
        new_pixel = tuple((value ^ key) for value in pixel)  # XOR each pixel component
        new_pixels.append(new_pixel)

  # Create new image with modified pixels
    new_image = Image.new(image.mode, image.size)
    new_image.putdata(new_pixels)
    return new_image

# Check if encrypted image exists before decrypting
    if os.path.exists(encrypted_image_path):
        encrypted_image = Image.open(encrypted_image_path)  # Load encrypted image
        print("Encrypted image loaded successfully.")

    # Decrypt Image
    decrypted_image = decrypt_image(encrypted_image, key)
    decrypted_image.save("decrypted_image.png")  # Save decrypted image
    decrypted_image.show()  # Display decrypted image
    print("Decryption completed. Decrypted image saved as 'decrypted_image.png'.")
else:
    print("Error: Encrypted image not found!")
