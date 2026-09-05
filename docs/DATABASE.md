# Database Schema

## Tables

### users
```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  username VARCHAR(50) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  currency INT DEFAULT 0,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  last_login TIMESTAMP
);
```

### houses
```sql
CREATE TABLE houses (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID UNIQUE NOT NULL REFERENCES users(id),
  weather_condition VARCHAR(50) DEFAULT 'clear',
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### items
```sql
CREATE TABLE items (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name VARCHAR(255) NOT NULL,
  category VARCHAR(50) NOT NULL, -- 'decoration', 'cosmetic', 'pet'
  price INT NOT NULL,
  description TEXT,
  image_url VARCHAR(500),
  is_available BOOLEAN DEFAULT true,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### house_inventory
```sql
CREATE TABLE house_inventory (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  house_id UUID NOT NULL REFERENCES houses(id),
  item_id UUID NOT NULL REFERENCES items(id),
  position_x INT,
  position_y INT,
  rotation INT DEFAULT 0,
  quantity INT DEFAULT 1,
  acquired_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### step_records
```sql
CREATE TABLE step_records (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id),
  steps INT NOT NULL,
  latitude DECIMAL(10, 8),
  longitude DECIMAL(11, 8),
  currency_earned INT,
  recorded_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### transactions
```sql
CREATE TABLE transactions (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id),
  transaction_type VARCHAR(50) NOT NULL, -- 'step_reward', 'purchase', 'refund'
  amount INT NOT NULL,
  item_id UUID REFERENCES items(id),
  description TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### weather_cache
```sql
CREATE TABLE weather_cache (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id),
  latitude DECIMAL(10, 8),
  longitude DECIMAL(11, 8),
  condition VARCHAR(50),
  temperature INT,
  humidity INT,
  wind_speed INT,
  description TEXT,
  cached_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  expires_at TIMESTAMP
);
```

## Indexes

```sql
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_username ON users(username);
CREATE INDEX idx_step_records_user ON step_records(user_id);
CREATE INDEX idx_step_records_date ON step_records(recorded_at);
CREATE INDEX idx_house_inventory_house ON house_inventory(house_id);
CREATE INDEX idx_transactions_user ON transactions(user_id);
CREATE INDEX idx_weather_cache_user ON weather_cache(user_id);
CREATE INDEX idx_weather_cache_expires ON weather_cache(expires_at);
```
