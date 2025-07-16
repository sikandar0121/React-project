import React, { useEffect, useRef, useState } from 'react';
import { gsap } from 'gsap';

function App() {
  // For Landing Section animation
  const paraRef = useRef();
  useEffect(() => {
    gsap.from(paraRef.current, {
      opacity: 0,
      y: 50,
      duration: 1,
      ease: 'power3.out',
    });
  }, []);

  // For FAQ
  const [activeIndex, setActiveIndex] = useState(null);
  const faqData = [
    { question: "यह क्या है?", answer: "यह एक FAQ सेक्शन का उदाहरण है।" },
    { question: "कैसे काम करता है?", answer: "क्लिक करने पर जवाब दिखता है।" },
  ];

  const toggleFAQ = (index) => {
    setActiveIndex(activeIndex === index ? null : index);
  };

  return (
    <div style={{ fontFamily: 'Segoe UI, Tahoma, Geneva, Verdana, sans-serif' }}>
      {/* Navbar */}
      <nav style={{
        display: 'flex', justifyContent: 'space-between', alignItems: 'center',
        padding: '15px 30px', backgroundColor: '#fff', boxShadow: '0 2px 4px rgba(0,0,0,0.1)', position: 'sticky', top: 0
      }}>
        <div style={{ fontWeight: 'bold', fontSize: '20px' }}>Logo</div>
        <div style={{ display: 'flex', gap: '15px' }}>
          <a href="#products" style={{ textDecoration: 'none', color: '#333' }}>Products</a>
          <a href="#faq" style={{ textDecoration: 'none', color: '#333' }}>FAQ</a>
        </div>
      </nav>

      {/* Landing Section */}
      <section style={{
        background: '#f9f9f9', minHeight: '80vh', padding: '60px 20px',
        textAlign: 'center'
      }}>
        <h1 style={{ fontSize: '2.5rem', fontWeight: 'bold' }}>Welcome to Luxury Landing</h1>
        <p ref={paraRef} style={{
          maxWidth: '600px', margin: '20px auto', color: '#555'
        }}>
          यह पहला पैराग्राफ है जिसमें एनिमेशन का इफेक्ट होगा, जो धीरे-धीरे शब्दों को life देता है।
        </p>
      </section>

      {/* Best Selling Products */}
      <section id="products" style={{ padding: '60px 20px', textAlign: 'center' }}>
        <h2 style={{ fontSize: '2rem', fontWeight: 'bold', marginBottom: '20px' }}>Best Selling Products</h2>
        <div style={{ display: 'flex', overflowX: 'auto', gap: '20px', justifyContent: 'center', padding: '10px' }}>
          {[1, 2, 3, 4].map((item) => (
            <div key={item} style={{
              minWidth: '200px', background: '#f2f2f2', padding: '20px',
              borderRadius: '10px', transition: 'transform 0.3s'
            }}
              onMouseEnter={e => e.currentTarget.style.transform = 'scale(1.05)'}
              onMouseLeave={e => e.currentTarget.style.transform = 'scale(1)'}
            >
              <p>Product {item}</p>
              <button style={{
                marginTop: '10px', padding: '8px 16px', background: '#000',
                color: '#fff', border: 'none', borderRadius: '5px'
              }}>
                View
              </button>
            </div>
          ))}
        </div>
      </section>

      {/* FAQ Section */}
      <section id="faq" style={{ background: '#f4f4f4', padding: '60px 20px', textAlign: 'center' }}>
        <h2 style={{ fontSize: '2rem', fontWeight: 'bold', marginBottom: '20px' }}>FAQ</h2>
        <div style={{ maxWidth: '600px', margin: 'auto', textAlign: 'left' }}>
          {faqData.map((item, index) => (
            <div key={index} style={{
              background: '#fff', margin: '10px 0', padding: '15px',
              borderRadius: '8px', boxShadow: '0 0 5px rgba(0,0,0,0.1)'
            }}>
              <button
                onClick={() => toggleFAQ(index)}
                style={{
                  width: '100%', textAlign: 'left', fontWeight: 'bold',
                  background: 'none', border: 'none', padding: '10px 0', cursor: 'pointer'
                }}
              >
                {item.question}
              </button>
              <div style={{
                maxHeight: activeIndex === index ? '100px' : '0',
                overflow: 'hidden', transition: 'max-height 0.5s ease', opacity: activeIndex === index ? 1 : 0
              }}>
                <p style={{ marginTop: '5px' }}>{item.answer}</p>
              </div>
            </div>
          ))}
        </div>
      </section>
    </div>
  );
}

export default App;
