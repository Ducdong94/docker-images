# docker-images
#!/bin/bash

# Thư mục chứa các file .tar
IMAGE_DIR="/path/to/your/directory"

# Kiểm tra xem thư mục có tồn tại không
if [ ! -d "$IMAGE_DIR" ]; then
    echo "Thư mục $IMAGE_DIR không tồn tại!"
    exit 1
fi

# Duyệt qua tất cả các file .tar trong thư mục
for image in "$IMAGE_DIR"/*.tar; do
    # Kiểm tra nếu không có file nào phù hợp
    if [ ! -f "$image" ]; then
        echo "Không tìm thấy file .tar nào trong thư mục $IMAGE_DIR"
        exit 1
    fi
    
    echo "Loading Docker image from $image..."
    docker load -i "$image"
    if [ $? -eq 0 ]; then
        echo "Loaded: $image"
    else
        echo "Failed to load: $image"
    fi
done

echo "Hoàn thành việc load tất cả Docker images."
