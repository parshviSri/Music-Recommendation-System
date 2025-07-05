# Music Recommendation System

A comprehensive music recommendation system that combines content-based filtering and popularity-based recommendations to suggest songs based on audio features and user preferences.

## 🎵 Project Overview

This project implements a hybrid music recommendation system that analyzes audio features from Spotify tracks to provide personalized song recommendations. The system combines:

- **Content-based filtering**: Uses audio features like danceability, energy, tempo, etc.
- **Popularity-based scoring**: Incorporates track popularity and recency
- **Hybrid recommendations**: Combines both approaches with configurable weights

## ✨ Features

### Core Functionality

- **Spotify API Integration**: Fetches real music data from Spotify's API
- **Audio Feature Analysis**: Analyzes 11 different audio features for each track
- **Content-Based Recommendations**: Finds similar songs based on audio characteristics
- **Hybrid Recommendation System**: Combines content similarity with popularity scoring
- **Configurable Parameters**: Adjustable recommendation count and weighting

### Audio Features Analyzed

- **Danceability**: How suitable a track is for dancing
- **Energy**: Perceptual measure of intensity and activity
- **Key**: Musical key of the track
- **Loudness**: Overall loudness in decibels
- **Mode**: Major or minor scale
- **Speechiness**: Presence of spoken words
- **Acousticness**: Confidence measure of acoustic vs electronic
- **Instrumentalness**: Predicts whether track contains vocals
- **Liveness**: Presence of audience in recording
- **Valence**: Musical positiveness
- **Tempo**: Estimated tempo in BPM

## 🚀 Getting Started

### Prerequisites

- Python 3.7+
- Spotify Developer Account
- Required Python packages (see Installation)

### Installation

1. **Clone the repository**

   ```bash
   git clone <repository-url>
   cd Music-Recommendation-System
   ```

2. **Install required packages**

   ```bash
   pip install pandas numpy scikit-learn spotipy requests
   ```

3. **Set up Spotify API credentials**
   - Go to [Spotify Developer Dashboard](https://developer.spotify.com/dashboard)
   - Create a new application
   - Get your `CLIENT_ID` and `CLIENT_SECRET`
   - Update the credentials in the notebook

### Spotify API Setup

1. **Get Access Token**

   ```python
   import base64
   import requests

   client_Id = "YOUR_CLIENT_ID"
   client_secret = "YOUR_CLIENT_SECRET"
   client_credentials = f"{client_Id}:{client_secret}"
   client_credentials_base64 = base64.b64encode(client_credentials.encode())

   token_url = "https://accounts.spotify.com/api/token"
   headers = {
       'Authorization': f'Basic {client_credentials_base64.decode()}'
   }
   data = {
       'grant_type': 'client_credentials'
   }
   response = requests.post(token_url, headers=headers, data=data)
   access_token = response.json().get("access_token")
   ```

## 📊 Data Structure

The system works with a comprehensive dataset containing:

### Track Information

- Track Name, Artists, Album Name
- Track ID, Album ID
- Popularity Score
- Release Date
- Duration, Explicit Content Flag
- External URLs

### Audio Features

- All 11 Spotify audio features (normalized 0-1)
- Duration in milliseconds
- Tempo in BPM

### Derived Features

- **Weight**: Recency-based popularity weight
- **Content Score**: Similarity score from content-based filtering
- **Hybrid Score**: Combined recommendation score

## 🔧 Usage

### 1. Content-Based Recommendations

```python
# Get recommendations based on audio features
recommendations = song_recommendation(track_id="your_track_id", number_recomendation=5)
```

### 2. Hybrid Recommendations

```python
# Get hybrid recommendations with popularity weighting
hybrid_recs = hybrid_recommendation_system(
    track_id="your_track_id",
    number_of_recommendation=5,
    alpha=0.5  # Weight for content vs popularity (0-1)
)
```

### 3. Data Preprocessing

The system automatically:

- Normalizes audio features using MinMaxScaler
- Calculates recency weights based on release dates
- Handles missing values and data validation

## 🧮 Algorithm Details

### Content-Based Filtering

1. **Feature Normalization**: All audio features are normalized to 0-1 scale
2. **Cosine Similarity**: Calculates similarity between track audio features
3. **Ranking**: Returns top N most similar tracks

### Hybrid Recommendation System

1. **Content Score**: Cosine similarity from content-based filtering
2. **Popularity Weight**: `Popularity × Recency_Weight`
3. **Hybrid Score**: `α × Content_Score + (1-α) × Popularity_Weight`
4. **Final Ranking**: Sorted by hybrid score

### Recency Weighting

```python
weight = 1 / (days_since_release + 1)
```

## 📈 Performance Metrics

The system provides:

- **Similarity Scores**: 0-1 range indicating audio feature similarity
- **Content Scores**: Normalized similarity scores
- **Hybrid Scores**: Combined recommendation scores
- **Popularity Integration**: Weighted by recency

## 🔍 Example Output

```
Track ID: c99bfd6d-efc3-4642-b4da-972cacb4e1f5
Hybrid Weighted Score: 50.45
Content Score: 0.783

Track ID: 1016af98-5741-4be5-a136-e69cd7e404e3
Hybrid Weighted Score: 50.26
Content Score: 0.489
```

## 🛠️ Technical Implementation

### Key Libraries Used

- **pandas**: Data manipulation and analysis
- **scikit-learn**: Machine learning algorithms and preprocessing
- **spotipy**: Spotify Web API wrapper
- **requests**: HTTP library for API calls
- **numpy**: Numerical computing

### Data Processing Pipeline

1. **Data Collection**: Fetch from Spotify API or generate mock data
2. **Preprocessing**: Handle missing values, normalize features
3. **Feature Engineering**: Calculate weights and derived features
4. **Similarity Calculation**: Compute cosine similarities
5. **Recommendation Generation**: Rank and return top matches

## 🔧 Configuration

### Adjustable Parameters

- `alpha`: Weight between content and popularity (0-1)
- `number_of_recommendation`: Number of songs to recommend
- `number_recomendation`: Alternative parameter name for consistency

### Data Sources

- **Real Data**: Spotify API integration
- **Mock Data**: Generated synthetic data for testing

## 📝 Future Enhancements

- [ ] User preference learning
- [ ] Collaborative filtering integration
- [ ] Real-time recommendation updates
- [ ] Web interface for recommendations
- [ ] Advanced audio feature analysis
- [ ] Genre-based filtering
- [ ] Mood-based recommendations

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Spotify Web API for providing music data
- Scikit-learn for machine learning algorithms
- Pandas community for data manipulation tools

## 📞 Support

For questions or support, please open an issue in the repository or contact the maintainers.

---

**Note**: This project is for educational and research purposes. Make sure to comply with Spotify's API terms of service when using real data.
