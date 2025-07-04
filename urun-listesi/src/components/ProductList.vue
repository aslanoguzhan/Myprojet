<template>
  <div class="product-list">
    <h1>Ürün Listesi</h1>
    
    <!-- Yeni Ürün Ekleme Formu -->
    <div class="add-product-form" v-if="showAddForm">
      <h3>{{ editingProduct ? 'Ürün Düzenle' : 'Yeni Ürün Ekle' }}</h3>
      <form @submit.prevent="saveProduct">
        <div class="form-group">
          <label>Ürün Adı:</label>
          <input 
            type="text" 
            v-model="currentProduct.name" 
            required 
            placeholder="Ürün adını giriniz"
          >
        </div>
        <div class="form-group">
          <label>Fiyat:</label>
          <input 
            type="number" 
            v-model="currentProduct.price" 
            required 
            min="0" 
            step="0.01"
            placeholder="Fiyat giriniz"
          >
        </div>
        <div class="form-group">
          <label>Kategori:</label>
          <select v-model="currentProduct.category" required>
            <option value="">Kategori seçiniz</option>
            <option value="Elektronik">Elektronik</option>
            <option value="Giyim">Giyim</option>
            <option value="Kitap">Kitap</option>
            <option value="Ev & Yaşam">Ev & Yaşam</option>
            <option value="Spor">Spor</option>
          </select>
        </div>
        <div class="form-group">
          <label>Açıklama:</label>
          <textarea 
            v-model="currentProduct.description" 
            placeholder="Ürün açıklaması (opsiyonel)"
            rows="3"
          ></textarea>
        </div>
        <div class="form-buttons">
          <button type="submit" class="btn btn-save">
            {{ editingProduct ? 'Güncelle' : 'Ekle' }}
          </button>
          <button type="button" @click="cancelEdit" class="btn btn-cancel">
            İptal
          </button>
        </div>
      </form>
    </div>

    <!-- Ürün Ekleme Butonu -->
    <div class="add-button-container" v-if="!showAddForm">
      <button @click="showAddProduct" class="btn btn-primary">
        ➕ Yeni Ürün Ekle
      </button>
    </div>

    <!-- Ürün Listesi -->
    <div class="products-container" v-if="products.length > 0">
      <div class="product-card" v-for="product in products" :key="product.id">
        <div class="product-header">
          <h3>{{ product.name }}</h3>
          <span class="product-price">{{ formatPrice(product.price) }} ₺</span>
        </div>
        <div class="product-body">
          <p class="product-category">
            <strong>Kategori:</strong> {{ product.category }}
          </p>
          <p class="product-description" v-if="product.description">
            <strong>Açıklama:</strong> {{ product.description }}
          </p>
        </div>
        <div class="product-actions">
          <button @click="editProduct(product)" class="btn btn-edit">
            ✏️ Düzenle
          </button>
          <button @click="deleteProduct(product.id)" class="btn btn-delete">
            🗑️ Sil
          </button>
        </div>
      </div>
    </div>

    <!-- Boş Liste Mesajı -->
    <div v-else class="empty-state">
      <p>Henüz hiç ürün eklenmemiş.</p>
      <button @click="showAddProduct" class="btn btn-primary">
        İlk ürününüzü ekleyin
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductList',
  data() {
    return {
      products: [
        {
          id: 1,
          name: 'iPhone 14 Pro',
          price: 15000,
          category: 'Elektronik',
          description: 'Apple\'ın en yeni telefonu, harika kamera özelliği'
        },
        {
          id: 2,
          name: 'Samsung Galaxy S23',
          price: 12000,
          category: 'Elektronik',
          description: 'Android\'in en güçlü telefonu'
        },
        {
          id: 3,
          name: 'MacBook Air M2',
          price: 25000,
          category: 'Elektronik',
          description: 'Hafif ve güçlü laptop'
        }
      ],
      showAddForm: false,
      editingProduct: null,
      currentProduct: {
        name: '',
        price: null,
        category: '',
        description: ''
      },
      nextId: 4
    }
  },
  methods: {
    showAddProduct() {
      this.showAddForm = true;
      this.editingProduct = null;
      this.resetCurrentProduct();
    },
    
    editProduct(product) {
      this.showAddForm = true;
      this.editingProduct = product;
      this.currentProduct = { ...product };
    },
    
    saveProduct() {
      if (this.editingProduct) {
        // Güncelleme
        const index = this.products.findIndex(p => p.id === this.editingProduct.id);
        if (index !== -1) {
          this.products[index] = { ...this.currentProduct };
        }
      } else {
        // Yeni ekleme
        const newProduct = {
          ...this.currentProduct,
          id: this.nextId++,
          price: parseFloat(this.currentProduct.price)
        };
        this.products.push(newProduct);
      }
      
      this.cancelEdit();
    },
    
    deleteProduct(productId) {
      if (confirm('Bu ürünü silmek istediğinizden emin misiniz?')) {
        this.products = this.products.filter(p => p.id !== productId);
      }
    },
    
    cancelEdit() {
      this.showAddForm = false;
      this.editingProduct = null;
      this.resetCurrentProduct();
    },
    
    resetCurrentProduct() {
      this.currentProduct = {
        name: '',
        price: null,
        category: '',
        description: ''
      };
    },
    
    formatPrice(price) {
      return new Intl.NumberFormat('tr-TR').format(price);
    }
  }
}
</script>

<style scoped>
.product-list {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

h1 {
  text-align: center;
  color: #2c3e50;
  margin-bottom: 30px;
}

/* Ürün Ekleme Formu */
.add-product-form {
  background: #f8f9fa;
  padding: 25px;
  border-radius: 10px;
  margin-bottom: 30px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

.add-product-form h3 {
  margin-bottom: 20px;
  color: #495057;
}

.form-group {
  margin-bottom: 15px;
}

.form-group label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
  color: #495057;
}

.form-group input,
.form-group select,
.form-group textarea {
  width: 100%;
  padding: 8px 12px;
  border: 1px solid #ced4da;
  border-radius: 5px;
  font-size: 14px;
  transition: border-color 0.3s;
}

.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #007bff;
  box-shadow: 0 0 0 2px rgba(0,123,255,.25);
}

.form-buttons {
  display: flex;
  gap: 10px;
  margin-top: 20px;
}

/* Butonlar */
.btn {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 14px;
  font-weight: bold;
  transition: all 0.3s;
  display: inline-flex;
  align-items: center;
  gap: 5px;
}

.btn:hover {
  transform: translateY(-1px);
  box-shadow: 0 2px 5px rgba(0,0,0,0.2);
}

.btn-primary {
  background-color: #007bff;
  color: white;
}

.btn-primary:hover {
  background-color: #0056b3;
}

.btn-save {
  background-color: #28a745;
  color: white;
}

.btn-save:hover {
  background-color: #1e7e34;
}

.btn-cancel {
  background-color: #6c757d;
  color: white;
}

.btn-cancel:hover {
  background-color: #545b62;
}

.btn-edit {
  background-color: #ffc107;
  color: #212529;
}

.btn-edit:hover {
  background-color: #e0a800;
}

.btn-delete {
  background-color: #dc3545;
  color: white;
}

.btn-delete:hover {
  background-color: #c82333;
}

/* Ürün Ekleme Butonu */
.add-button-container {
  text-align: center;
  margin-bottom: 30px;
}

/* Ürün Kartları */
.products-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 20px;
  margin-top: 20px;
}

.product-card {
  background: white;
  border: 1px solid #e9ecef;
  border-radius: 10px;
  padding: 20px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
  transition: transform 0.3s, box-shadow 0.3s;
}

.product-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 20px rgba(0,0,0,0.15);
}

.product-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 15px;
  border-bottom: 1px solid #e9ecef;
  padding-bottom: 10px;
}

.product-header h3 {
  margin: 0;
  color: #2c3e50;
  font-size: 18px;
}

.product-price {
  background: #e3f2fd;
  color: #1976d2;
  padding: 5px 10px;
  border-radius: 20px;
  font-weight: bold;
  font-size: 16px;
}

.product-body {
  margin-bottom: 15px;
}

.product-category,
.product-description {
  margin: 8px 0;
  color: #6c757d;
  line-height: 1.4;
}

.product-actions {
  display: flex;
  gap: 10px;
  justify-content: flex-end;
}

/* Boş Durum */
.empty-state {
  text-align: center;
  padding: 60px 20px;
  color: #6c757d;
}

.empty-state p {
  font-size: 18px;
  margin-bottom: 20px;
}

/* Responsive Tasarım */
@media (max-width: 768px) {
  .products-container {
    grid-template-columns: 1fr;
  }
  
  .product-header {
    flex-direction: column;
    align-items: flex-start;
    gap: 10px;
  }
  
  .product-actions {
    justify-content: center;
  }
  
  .form-buttons {
    flex-direction: column;
  }
}
</style>