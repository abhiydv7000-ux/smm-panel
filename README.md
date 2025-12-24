# smm-panel
trusted followers 
smm-panel/
 ├─ server.js
 ├─ models/
 │   ├─ User.js
 │   ├─ Order.js
 ├─ routes/
 │   ├─ auth.js
 │   ├─ order.js
 ├─ services/
 │   ├─ providerApi.js
 └─ .env
// models/User.js
const mongoose = require("mongoose");

const UserSchema = new mongoose.Schema({
  username: String,
  email: String,
  password: String,
  balance: { type: Number, default: 0 },
  role: { type: String, default: "user" }
});

module.exports = mongoose.model("User", UserSchema);
// models/Order.js
const mongoose = require("mongoose");

const OrderSchema = new mongoose.Schema({
  userId: String,
  service: String,
  link: String,
  quantity: Number,
  status: { type: String, default: "Pending" },
  providerOrderId: String
});

module.exports = mongoose.model("Order", OrderSchema);
// services/providerApi.js
const axios = require("axios");

async function createProviderOrder(serviceId, link, quantity) {
  const response = await axios.post("https://provider-api.com/api/v2", {
    key: process.env.PROVIDER_API_KEY,
    action: "add",
    service: serviceId,
    link: link,
    quantity: quantity
  });

  return response.data;
}

module.exports = { createProviderOrder };
// routes/order.js
const express = require("express");
const router = express.Router();
const Order = require("../models/Order");
const { createProviderOrder } = require("../services/providerApi");

router.post("/create", async (req, res) => {
  const { service, link, quantity } = req.body;

  const providerResponse = await createProviderOrder(
    service,
    link,
    quantity
  );

  const order = new Order({
    userId: req.user.id,
    service,
    link,
    quantity,
    providerOrderId: providerResponse.order
  });

  await order.save();
  res.json({ success: true, order });
});

module.exports = router;
// server.js
require("dotenv").config();
const express = require("express");
const mongoose = require("mongoose");

const app = express();
app.use(express.json());

mongoose.connect(process.env.MONGO_URI);

app.use("/api/order", require("./routes/order"));

app.listen(5000, () => {
  console.log("SMM Panel running on port 5000");
});
