const tarotList = [
  { name: "The Fool", meaning: "Khởi đầu, sự tự do, trải nghiệm mới." },
  { name: "The Magician", meaning: "Sáng tạo, tiềm năng, kiểm soát vận mệnh." },
  { name: "The High Priestess", meaning: "Trực giác, bí mật, trí tuệ tiềm ẩn." },
  { name: "The Empress", meaning: "Tình mẫu tử, nuôi dưỡng, sự phong phú." },
  { name: "The Emperor", meaning: "Quyền lực, trật tự, ổn định." },
  { name: "The Hierophant", meaning: "Truyền thống, hướng dẫn tinh thần." },
  { name: "The Lovers", meaning: "Tình yêu, mối quan hệ, lựa chọn lớn." },
  { name: "The Chariot", meaning: "Chiến thắng, kiểm soát bản thân, hành động." },
  { name: "Strength", meaning: "Sự dũng cảm, kiên trì, nội lực mạnh mẽ." },
  { name: "The Hermit", meaning: "Tự chiêm nghiệm, tìm kiếm chân lý." },
  { name: "Wheel of Fortune", meaning: "Số phận, thay đổi, cơ hội." },
  { name: "Justice", meaning: "Công lý, sự thật, hậu quả." },
  { name: "The Hanged Man", meaning: "Hy sinh, cái nhìn khác biệt, buông bỏ." },
  { name: "Death", meaning: "Kết thúc, sự thay đổi lớn, tái sinh." },
  { name: "Temperance", meaning: "Cân bằng, điều độ, hòa hợp." },
  { name: "The Devil", meaning: "Ràng buộc, cám dỗ, nghiện ngập." },
  { name: "The Tower", meaning: "Sụp đổ, thay đổi đột ngột, khai sáng." },
  { name: "The Star", meaning: "Hy vọng, chữa lành, cảm hứng." },
  { name: "The Moon", meaning: "Ảo giác, mơ hồ, trực giác." },
  { name: "The Sun", meaning: "Thành công, hạnh phúc, rõ ràng." },
  { name: "Judgement", meaning: "Thức tỉnh, hồi sinh, đánh giá." },
  { name: "The World", meaning: "Hoàn thành, trọn vẹn, du hành." }
];

function getZodiac(month) {
  const elements = ["Kim", "Mộc", "Thủy", "Hỏa", "Thổ"];
  return elements[month % 5];
}

function getNumerology(d, m, y) {
  let total = d + m + y;
  while (total > 9) {
    total = total.toString().split('').reduce((a, b) => a + Number(b), 0);
  }
  return total;
}

function luanGiai() {
  const name = document.getElementById("name").value.trim();
  const birth = document.getElementById("birth").value;
  const output = document.getElementById("output");

  if (!name || !birth) {
    alert("Vui lòng nhập đầy đủ họ tên và ngày sinh!");
    return;
  }

  const [year, month, day] = birth.split("-").map(Number);
  const zodiac = getZodiac(month);
  const numerology = getNumerology(day, month, year);
  const tarotIndex = (name.length + day + month + year) % tarotList.length;
  const tarot = tarotList[tarotIndex];

  output.innerHTML = `
    <p><strong>👤 Họ tên:</strong> ${name}</p>
    <p><strong>📅 Ngày sinh:</strong> ${day}/${month}/${year}</p>
    <p><strong>🌱 Tử vi:</strong> Bạn thuộc mệnh <strong>${zodiac}</strong> – đại diện cho tính cách, hành động và vận mệnh riêng biệt.</p>
    <p><strong>🔢 Thần số học:</strong> Số chủ đạo <strong>${numerology}</strong> – mang ý nghĩa đặc biệt về tính cách và con đường phát triển cá nhân.</p>
    <p><strong>🃏 Tarot:</strong> Lá bài hôm nay là <strong>${tarot.name}</strong> – ${tarot.meaning}</p>
  `;
  output.style.display = "block";
}
