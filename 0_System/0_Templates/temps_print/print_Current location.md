<%*
const getLocation = async () => {
    try {
        const response = await fetch("https://ipapi.co/json/");
        if (!response.ok) throw new Error("Failed to fetch location data");

        const data = await response.json();
        return `${data.city}, ${data.country_name}`;
    } catch (error) {
        console.error("Error fetching location:", error);
        return "Unknown Location";
    }
};

tR += await getLocation();
-%>
