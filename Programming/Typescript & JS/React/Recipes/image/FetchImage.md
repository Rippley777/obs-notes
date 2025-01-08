This is created from [[Uploading Images in mongoose]]


```import React, { useState, useEffect } from 'react';

const ImageViewer = ({ imageId }) => {
    const [imageUrl, setImageUrl] = useState('');
    const [error, setError] = useState('');

    useEffect(() => {
        // Function to fetch the image
        const fetchImage = async () => {
            try {
                const response = await fetch(`/image/${imageId}`);
                if (!response.ok) {
                    throw new Error('Image not found');
                }
                const imageBlob = await response.blob();
                const imageObjectURL = URL.createObjectURL(imageBlob);
                setImageUrl(imageObjectURL);
            } catch (err) {
                setError(err.message);
            }
        };

        if (imageId) {
            fetchImage();
        }
    }, [imageId]);  // Depend on imageId to refetch when it changes

    return (
        <div>
            {error ? (
                <p>Error: {error}</p>
            ) : (
                imageUrl ? <img src={imageUrl} alt="Fetched from server" style={{ maxWidth: '100%' }} /> : <p>Loading image...</p>
            )}
        </div>
    );
};

export default ImageViewer;

```