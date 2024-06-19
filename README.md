#include <SFML/Graphics.hpp>

constexpr int windowWidth = 800;
constexpr int windowHeight = 600;
constexpr int pixelSize = 5; // Size of each pixel square

int main() {
    sf::RenderWindow window(sf::VideoMode(windowWidth, windowHeight), "Pixel Painter");

    // Create an image to represent the pixel grid
    sf::Image image;
    image.create(windowWidth / pixelSize, windowHeight / pixelSize, sf::Color::White); // Initialize with white pixels

    // Create a texture and sprite to display the image
    sf::Texture texture;
    texture.loadFromImage(image);
    sf::Sprite sprite(texture);

    // Main loop
    while (window.isOpen()) {
        sf::Event event;
        while (window.pollEvent(event)) {
            if (event.type == sf::Event::Closed)
                window.close();
            else if (event.type == sf::Event::MouseButtonPressed && event.mouseButton.button == sf::Mouse::Left) {
                // Calculate the position of the pixel clicked
                int x = event.mouseButton.x / pixelSize;
                int y = event.mouseButton.y / pixelSize;
                
                // Set the color of the pixel in the image
                image.setPixel(x, y, sf::Color::Black); // For simplicity, set to black when left mouse button is clicked
                texture.loadFromImage(image); // Update the texture
            }
        }

        window.clear(sf::Color::White);
        window.draw(sprite);
        window.display();
    }

    return 0;
}
