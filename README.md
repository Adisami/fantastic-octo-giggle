from PIL import Image, ImageDraw, ImageFont

def create_image(text, image_size=(800, 600), bg_color=(255, 255, 255), text_color=(0, 0, 0), font_size=50):
    # Create a blank image with the specified background color
    img = Image.new('RGB', image_size, color=bg_color)
    
    # Initialize ImageDraw
    draw = ImageDraw.Draw(img)
    
    # Load a font
    try:
        font = ImageFont.truetype("arial.ttf", font_size)
    except IOError:
        font = ImageFont.load_default()

    # Calculate the width and height of the text to be added
    text_width, text_height = draw.textsize(text, font=font)
    
    # Calculate X, Y position of the text
    text_x = (image_size[0] - text_width) // 2
    text_y = (image_size[1] - text_height) // 2
    
    # Add text to image
    draw.text((text_x, text_y), text, fill=text_color, font=font)
    
    # Save the image
    img.save("generated_image.png")
    print("Image saved as generated_image.png")

# Example usage
if __name__ == "__main__":
    text = "Hello, World!"
    create_image(text, image_size=(1024, 768), bg_color=(135, 206, 250), text_color=(255, 255, 255), font_size=70)
