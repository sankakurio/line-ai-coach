import { buffer } from 'micro';

export const config = {
  api: {
    bodyParser: false,
  },
};

export default async function handler(req, res) {
  if (req.method !== 'POST') {
    return res.status(405).send('Method Not Allowed');
  }

  const buf = await buffer(req);
  const body = JSON.parse(buf.toString());

  console.log("✅ Webhook受信成功");
  console.log(JSON.stringify(body, null, 2));

  return res.status(200).send('OK');
}
